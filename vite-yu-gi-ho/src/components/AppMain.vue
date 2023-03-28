<script>
import axios from 'axios'
export default{
    components:{
       name:'AppMain',
    },
    data(){
        return{
            cards:[],
            archetypes:[],
            selectedArchetype: ''
        }
    },
    created(){
        this.fetchArchetypes()
    },
    methods: {
        fetchArchetypes() {
        axios.get('https://db.ygoprodeck.com/api/v7/archetypes.php')
        .then(response => {
          this.archetypes = response.data
        })
        .catch(error => console.error(error))
        },
        fetchCardsByArchetype(archetype) {
        axios.get(`https://db.ygoprodeck.com/api/v7/cardinfo.php?archetype=${archetype}`)
        .then(response => {
          this.cards = response.data.data
          const headerCard = document.querySelector('.header_card')
        headerCard.textContent = `Found ${this.cards.length} cards`
        })
        .catch(error => console.error(error))
        }
    },
}
</script>
<template>
<div>
    <select class="select" id="Tipo" v-model="selectedArchetype" @change="fetchCardsByArchetype(selectedArchetype)">
        <option  v-for="archetype in archetypes" :value="archetype.archetype_name">{{ archetype.archetype_name }}></option>
    </select>
</div>
<div class="main_container">
<div class="header_card"></div>
<div class="container_cards">
    <div class="cards" v-for="card in cards">
        <div class="card">
            <img :src="card.card_images[0].image_url" alt="">
        </div>
        <div class="info_card">
            <h3>{{ card.name }}</h3>
            <p>{{ card.archetype }}</p>
        </div>
    </div>
</div>
</div>
</template>
<style lang="scss" scoped>
.select{
    margin-left: 100px;
    margin-top: 30px;
    margin-bottom: 30px;
}
.header_card{
    color: white;
    background-color: black;
    padding: 20px;
    margin-left: 10px;
    margin-right: 10px;
}
.main_container{
    margin-left: 60px;
    margin-right: 60px;
    background-color: white;
    padding: 40px;
}
.container_cards{
    display: flex;
    flex-wrap: wrap;
    background-color: white;
}
.cards{
    width: calc(100% /5);
    margin-bottom: 25px;
}
.card img{
    width: 100%;
    display: block;
}
.card{
    padding-left: 10px;
    padding-right: 10px;;
}
.info_card{
    text-align: center;  
    background-color: #d48f38;
    margin-left: 10px;
    margin-right: 10px;  
}
.info_card{
    h3{
        padding: 10px 0;
    }
    p{
        padding: 10px 0;
    }
}
</style>
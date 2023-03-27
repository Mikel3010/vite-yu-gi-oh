<script>
import axios from 'axios'
export default{
    components:{
       name:'AppMain',
    },
    data(){
        return{
            cards:[],
            img:[]
        }
    },
    created(){
        axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php')
        .then((response)=>{
            console.log(response)
            this.cards= response.data.data
            this.img = response.data.data.card_images
        })
    }
}
</script>
<template>
<div>
    <select name="Tipo" id="Tipo" class="select">
        <option value="Alien">Alien</option>
        <option value="Magic">Magic</option>
        <option value="Fire">Fire</option>
    </select>
</div>
<div class="main_container">
<div class="header_card">Found 39 cards</div>
<div class="container_cards">
    <div class="cards" v-for="card in cards">
        <div class="card">
            <img src="" alt="">
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
    padding: 15px;
}
.main_container{
    margin-left: 50px;
    margin-right: 50px;
    background-color: white;
    padding: 40px;
}
.container_cards{
    display: flex;
    flex-wrap: wrap;
}
.cards{
    background-color: #d48f38;
    width: calc(100% /5);
}
</style>
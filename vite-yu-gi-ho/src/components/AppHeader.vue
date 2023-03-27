<script>
export default{
    components:{
       name:'AppHeader',
    }
}
</script>
<template>
<div class="container_header">
    <div class="logo">
        <img src="../../public/Yu-Gi-Oh!.svg" alt="">
    </div>
    <div class="titolo">
        <h1>Yu-Gi-Ho Api</h1>
    </div>
</div>
</template>
<style lang="scss" scoped>
.container_header{
    height: 6.25rem;
    display: flex;
    align-items: center;
}
.logo{
    height: 1.875rem;
    width: 80px;
    margin-left: 30px;
    margin-right: 20px;
}
.logo img{
    width: 100%;
}

</style>
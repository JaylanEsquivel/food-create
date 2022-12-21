<template>
    <div id="banner-main">
        <h1>Food Create</h1>
    </div>
</template>
<script>
    export default {
        name: 'Banner',
    }
</script>
<style scoped>
    #banner-main{
        background-image: url("/public/img/burger.jpg");
        display: flex;
        align-items: center;
        justify-content: flex-start;
        background-size: cover;
        background-position: 0 -250px;
        height: 500px;
    }
    h1{
        background-color: #f2ba0d;
        padding: 20px;
        font-size: 60px;
    }
    @media screen and (max-width: 500px) {
        #banner-main{
            background-position: 0px;
            background-repeat: no-repeat;
            height: 300px;
        }
        h1{
            font-size: 25px;
        }
    }


</style>
<template>
  <Navbar :logo="logo_src" :alt="app_name" />
  <router-view/>
  <Footer />
</template>
<script>
import Navbar from './components/Navbar.vue';
import Footer from './components/Footer.vue';
  
  export default {
    components: {
      Navbar, Footer
    },
    data() { 
      return {
        logo_src: '/img/logo.png',
        app_name: 'Food Create'
      }
    }
  }

</script>

<style>
    * {
      padding: 0;
      margin: 0;
      box-sizing: border-box;
      font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    }

    .main-container{
      padding: 20px;
      min-height: 250px;
      background-color: #fbfbfb;
    }

    h1{
      color: #222;
      text-align: center;
      margin-top: 20px;
      margin-bottom: 20px;
    }
    @media screen and (max-width: 500px) {
      h1{
        font-size: 28px;
      }
    }

</style>

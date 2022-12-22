<template>

   <Banner />
  <div class="main-container">
      <h1>Monte um Hambúrger do seu Jeito!</h1>

      <BurguerForm />
  </div>
</template>

<script>
    import Banner from '../components/Banner.vue';
    import BurguerForm from '@/components/BurguerForm.vue';

    export default {
        name: 'Home',
        components: {
          Banner, BurguerForm
        },
        data() { 
          return {
              
          }
        }
    }
</script>
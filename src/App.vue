<template>
  <header>
    <Navbar :logo="logo_src" :alt="app_name"/>
  </header>
  <RouterView />
  <Footer />
</template>

<script >

  import { RouterLink, RouterView } from 'vue-router'
  import Navbar from './components/navbar.vue';
  import Footer from './components/Footer.vue';

  export default {
    components: {
      Navbar,
      Footer,
    },

    data() {
      return {
        logo_src: "/img/logo.png",
        app_name: "You Make Burger"
      }
    }
  }

</script>


<style>
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Verdana, Geneva, Tahoma, sans-serif;

  }

  .main_container{
    width: 90%;
    margin: 1vh 5%; 
    min-height: 78vh;
    border-radius: 10px;
    box-shadow: 0 0 10px 1px rgba( 0, 0, 0, .3);
  }

  .main_container h1{
    text-align: center;
    font-size: 42px;
    margin-bottom: 50px;
    color: #222;
  }

  h1 span{
    font-size: 52px;
    color: #FCBA03;
  }

</style>

<template>
  <main class="main_container">
    <Banner />
    <h1><span>|</span>Monte seu Hamburguer</h1>
    <formulario />
  </main>
</template>

<script>
  import Banner from '../components/Banner.vue';
  import Formulario from '../components/Formulario.vue';

  export default {
    name: "Home",
    components:{
      Banner,
      Formulario,
    }
  }
</script>
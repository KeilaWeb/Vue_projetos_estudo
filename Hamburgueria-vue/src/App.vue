<template>
  <Navegacao :logo="logo_src" :alt="app_name" />
  <router-view/>
  <Rodape />
</template>

<script>
import Navegacao from './components/Navegacao.vue';
import Rodape from './components/Rodape.vue';

export default {
  components: {
    Navegacao,
    Rodape
  },
  data() {
    return {
      logo_src: "/img/logo.png",
      app_name: "Faça seu Burger"
    }
  }
}
</script>

<style scope>
/*
  Cor destaque: #E4700C
  Marrom: #792F20
*/

  * {    
    font-family: cursive;   
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  .main-container {
    min-height: 600px;
    padding-top: 100px;
  }

  h1 {
    font-size: 42px;
    line-height: 1.4em;
  }
</style>

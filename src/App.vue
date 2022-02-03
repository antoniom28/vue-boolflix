<template>
  <div id="app">
    <Header @loadFilmApp="loadFilm" />
    <Main :inputFilm="loadedFilm" 
    :inputType="inputType"
     />
    
    <Footer />
  </div>
</template>

<script>
import Main from './components/macro/Main.vue'
import Footer from './components/macro/Footer.vue'
import Header from './components/macro/Header.vue'

export default {
  name: 'App',
  data(){
    return{
      loadedFilm : [],
      inputType : null,
    }
  },
  components: {
    Main,
    Footer,
    Header,
  },
  methods: {
    loadFilm(film,type){
      this.loadedFilm = film;
      this.inputType = type.toUpperCase();
    },
  },
}
</script>

<style lang="scss">
@import './assets/style/globals.scss';

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>

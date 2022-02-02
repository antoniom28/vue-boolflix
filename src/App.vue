<template>
  <div id="app">
    <Header @loadFilm="loadFilm" />
    <Main :inputFilm="loadedFilm" />
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
    }
  },
  components: {
    Main,
    Footer,
    Header,
  },
  methods: {
    loadFilm(film){
      this.loadedFilm = film;
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

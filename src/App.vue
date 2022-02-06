<template>
  <div id="app">
    <Header @loadFilmApp="loadFilm" />
    <Main :inputText="inputText" 
    :inputType="inputType"
    :language="language"
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
      inputText : "",
      inputType : null,
      language: "it",
    }
  },
  components: {
    Main,
    Footer,
    Header,
  },
  methods: {
    loadFilm(input,type,lang){
      this.inputText = input;
      this.inputType = type.toUpperCase();
      this.language = lang;
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

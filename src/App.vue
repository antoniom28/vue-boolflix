<template>
  <div id="app">
    <Header msg="msg header"/>
    <Main />
    <Footer />
  </div>
</template>

<script>
import Main from './components/macro/Main.vue'
import Footer from './components/macro/Footer.vue'
import Header from './components/macro/Header.vue'

export default {
  name: 'App',
  components: {
    Main,
    Footer,
    Header,
  }
}
</script>

<style lang="scss">
@import './assets/style/globals.scss';

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>

<template>
  <header class="container-header">
    <div class="nav-left">
      <h2>BOOLFLIX</h2>
      <div>
        <p class="menuOption home" @click="getInputType('home')"> Home </p>
        <p class="menuOption movie" @click="getInputType('movie')"> Film </p>
        <p class="menuOption tv" @click="getInputType('tv')"> Serie TV </p>
      </div>
    </div>
    <Cerca v-if="showSearch" @searchFilm="get" />
  </header>
</template>

<script>
import Cerca from "../common/Cerca.vue";

export default {
  name: "Header",
  data() {
    return {
      page: 2,
      inputType: "home",
      prevInputType: null, //evita la chiamata su axios allo spam sulla categoria
      inputText: null,
      showSearch: false,
      language: "it",
    };
  },
  components: {
    Cerca,
  },
  methods: {
    noFocusOption(focus) {
      for (let i = 0; i < focus.length; i++) focus[i].style.color = "grey";

      if (this.inputText != null)
        if (this.prevInputType != this.inputType)
          this.get(this.inputText,this.language);
    },
    getInputType(type) {
      this.prevInputType = this.inputType;
      this.inputType = type;
      if (type != "home") this.showSearch = true;
      else this.showSearch = false;
      this.noFocusOption(this.$el.querySelectorAll(`.menuOption`));
      this.$el.querySelector(`.menuOption.${type}`).style.color = "white";
    },
    get(input,lang) {
      this.inputText = input;
      this.language = lang;
      this.$emit("loadFilmApp", this.inputText, this.inputType, this.language);
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../../assets/style/partials/variables.scss";

.menuOption {
  color: grey;
}

.home {
  color: white;
}

p {
  margin: 0 15px;
  cursor: pointer;
}

@media screen and (min-width:601px) {
  header{
    flex-direction:row!important;
  }

  h2, div{
    margin: 0!important;
  }
  
  .nav-left{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
}

h2, div{
    margin: 8px;
}

header {
  display: flex;
  justify-content: space-between;
  text-align: center;
  align-items: center;
  background: $bg_main_color;
  min-height: 60px;
  padding: 20px 25px 10px 25px;
  flex-direction:column;

  h2 {
    color: $text_color;
  }
}
</style>
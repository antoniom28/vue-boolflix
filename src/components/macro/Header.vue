<template>
  <header class="container-header">
    <div>
      <h2>BOOLFLIX</h2>
      <p class="menuOption home" @click="getInputType('home')">Home</p>
      <p class="menuOption movie" @click="getInputType('movie')">Film</p>
      <p class="menuOption tv" @click="getInputType('tv')">Serie TV</p>
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
          this.get(this.inputText);
    },
    getInputType(type) {
      this.prevInputType = this.inputType;
      this.inputType = type;
      if (type != "home") this.showSearch = true;
      else this.showSearch = false;
      this.noFocusOption(this.$el.querySelectorAll(`.menuOption`));
      this.$el.querySelector(`.menuOption.${type}`).style.color = "white";
    },
    get(input) {
      this.inputText = input;
      this.$emit("loadFilmApp", this.inputText, this.inputType);
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

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: $bg_main_color;
  height: 60px;
  padding: 20px 25px 10px 25px;

  h2 {
    color: $text_color;
  }
}
</style>
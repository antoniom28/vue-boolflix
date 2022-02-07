<template>
  <main class="container">
    <div>
      <Select
        :optionArr="optionArr"
        :filterSelect="filterSelect"
        @getFilterSelect="getFilterSelect"
        :inputType="inputType"
      />

      <h2 
        v-if="this.inputType && this.inputType != 'HOME'" 
        class="full-w"
      >
        Ricerca per : {{ this.inputType }}
      </h2>

      <Home v-show="showHome()" />

      <Movie 
        v-show="inputType == 'MOVIE'"
        :filterSelect="filterSelect"
        :inputText="inputText"
        :inputType="inputType"
        :language="language"
        call= 'movie'
      />

      <Movie 
        v-show="inputType == 'TV'"
        :filterSelect="filterSelect"
        :inputText="inputText"
        :inputType="inputType"
        :language="language"
        call= 'tv'
      />
    </div>
  </main>
</template>

<script>
import Home from "../section/Home.vue";
import Movie from "../section/Movie.vue";
import Select from "../common/Select.vue";

export default {
  name: "Main",
  data() {
    return {
      optionArr: [],
      filterSelect: [],
    };
  },
  components: {
    Select,
    Home,
    Movie,
  },
  props: {
    inputText: String,
    inputType: String,
    language: String,
  },
  methods: {
    showHome() {
      if (
        this.inputType == "" ||
        this.inputType == null ||
        this.inputType == "HOME"
      )
        return true;
      return false;
    },
    getFilterSelect(filter) {
      this.filterSelect = filter;
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../../assets/style/partials/variables.scss";
main {
  background-color: $bg_sec_color;
  min-height: calc(100vh - 60px);
}
</style>
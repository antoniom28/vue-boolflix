<template>
  <main class="container">
    <div>
      <Select
        :optionArr="optionArr"
        :filterSelect="filterSelect"
        @getFilterSelect="getFilterSelect"
        :inputType="inputType"
      />

      <h2 v-if="this.inputType && this.inputType != 'HOME'" class="full-w">
        Ricerca per : {{ this.inputType }}
      </h2>

      <Home v-show="showHome()" />

      <!-- movie e serietv sono praticamente uguali
      ma con url diversa, in questo modo l'axios in movie e tv viene
      chiamato solo quando scriviamo in input, e non sullo switch 
      o sul cambio filtro
      -->
      <Movie 
        v-show="inputType == 'MOVIE'"
        :filterSelect="filterSelect"
        :inputText="inputText"
        :inputType="inputType"
      />

      <SerieTv 
        v-show="inputType == 'TV'"
        :filterSelect="filterSelect"
        :inputText="inputText"
        :inputType="inputType"
      />
    </div>
  </main>
</template>

<script>
import Home from "../section/Home.vue";
import Movie from "../section/Movie.vue";
import SerieTv from "../section/SerieTv.vue";
import Select from "../common/Select.vue";

export default {
  name: "Main",
  data() {
    return {
      optionArr: [],
      filterSelect: 0,
    };
  },
  components: {
    Select,
    Home,
    Movie,
    SerieTv,
  },
  props: {
    inputText: String,
    inputType: String, 
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

.full-w {
  width: 100%;
  margin-top: 5px;
  text-align: center;
  color: white;
}

</style>
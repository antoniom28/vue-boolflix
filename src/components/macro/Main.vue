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
        v-if="filterSelectName.length >= 4"
        class="full-w"
      >
          Search For : Multiple Genre
      </h2>

      <h2 
        v-else-if="this.inputType && this.inputType != 'HOME' && filterSelectName.length > 0" 
        class="full-w"
      >
        Search For : 
        <h3 
          v-for="(name,index) in filterSelectName"
          :key="'filter'+index"
        > 
          {{ name }}<span v-if="index != filterSelectName.length - 1">, &nbsp;</span>
        </h3>
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
      filterSelectName : "",
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
    getFilterSelect(filterId , filterName) {
      this.filterSelect = filterId;
      this.filterSelectName = filterName;
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../../assets/style/partials/variables.scss";
main {
  //background-color: $bg_sec_color;
  background-image: url(../../assets/img/background.jpg);
    background-size: cover;
    min-height: calc(100vh - 60px);
    background-attachment: fixed;
}

h2{
  text-shadow: 2px 2px 3px black;
}
</style>
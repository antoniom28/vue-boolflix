<template>
  <main class="container">
    <ul>
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
    <!--
      <div v-show="filterError()" class="empty">
        Cerca un Titolo o Applica un filtro per mostrare i risultati!!
        {{ inputType }}
      </div> -->
    </ul>
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
    filterError() {
      if (
       // this.filterFilm.length == 0 &&
        this.inputType != "HOME" &&
        this.inputType != null
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

ul {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: flex-start;
}

.full-w {
  width: 100%;
  margin-top: 5px;
  text-align: center;
  color: white;
}

.empty {
  color: white;
  font-size: 1.5em;
  margin: 20px;
}
</style>
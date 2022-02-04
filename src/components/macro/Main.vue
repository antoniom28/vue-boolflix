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

      <Home
        v-show="inputType == '' || inputType == null || inputFilm.length == 0"
      />

      <ul v-show="inputType != '' && inputType != null">
        <FilmCards
          v-for="(film, index) in filterFilm"
          :key="index"
          :films="film"
          :inputType="inputType"
        />
      </ul>

      <div
        v-show="
          filterFilm.length == 0 && (inputType == '' || inputType == null)
        "
        class="empty"
      >
        Cerca un Titolo o Applica un filtro per mostrare i risultati!!
      </div>
    </ul>
  </main>
</template>

<script>
import FilmCards from "../section/FilmCards.vue";
import Home from "../section/Home.vue";
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
    FilmCards,
    Select,
    Home,
  },
  props: {
    inputFilm: Array,
    inputType: String,
  },
  computed: {
    filterFilm: function () {
      let film = [];
      if (this.filterSelect != "" && this.filterSelect) {
        for (let i = 0; i < this.inputFilm.length; i++) {
          for (let j = 0; j < this.inputFilm[i].genre_ids.length; j++) {
            if (this.filterSelect == this.inputFilm[i].genre_ids[j])
              film.push(this.inputFilm[i]);
          }
        }
        return film;
      } else return this.inputFilm;
    },
  },
  methods: {
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
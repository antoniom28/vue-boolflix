<template>
  <ul id="home">
    <FilmCards v-for="(film, index) in ratedFilm" :key="index" :films="film" />
  </ul>
</template>

<script>
import FilmCards from "../section/FilmCards.vue";
import axios from "axios";

export default {
  name: "Home",
  data() {
    return {
      ratedFilm: [],
    };
  },
  components: {
    FilmCards,
  },
  created: function () {
    if (this.ratedFilm.length == 0) this.getRatedFilm();
  },
  methods: {
    async getRatedFilm() {
      let response = await this.makeAxiosCall(
        `https://api.themoviedb.org/3/movie/popular`
      );
      this.ratedFilm = response.data.results;
    },
    makeAxiosCall(url) {
      console.log("call of axios from Home");
      return axios.get(url, {
        params: {
          api_key: "8de7c27ea07119ebc4c79cbfffb7d231",
        },
      });
    },
  },
};
</script>

<style lang="scss" scoped>
ul {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: flex-start;
}
</style>
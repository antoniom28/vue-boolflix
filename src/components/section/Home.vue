<template>
  <ul class="section-list" id="home">
    <h1 class="full-w">TOP RATED MOVIES</h1>

    <FilmCards 
      v-for="(film, index) in ratedFilm" 
      :key="index" 
      :films="film" 
      home-page="home-page"
    />
    <div class="full-w load-more">
      <span @click="loadMore()">
        LOAD MORE
        <i class="fas fa-angle-double-down"></i>
      </span>
    </div>
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
      page: 1,
    };
  },
  components: {
    FilmCards,
  },
  created: function () {
    if (this.ratedFilm.length == 0) this.getRatedFilm();
  },
  methods: {
    loadMore() {
      console.log("load");
      this.page++;
      this.getRatedFilm();
    },
    async getRatedFilm() {
      let response = await this.makeAxiosCall(
        `https://api.themoviedb.org/3/movie/popular`,
        this.page
      );
      console.log(response.data.total_pages);
      this.ratedFilm.push(...response.data.results);
    },
    makeAxiosCall(url, Npage) {
      console.log("call of axios from Home");
      return axios.get(url, {
        params: {
          api_key: "8de7c27ea07119ebc4c79cbfffb7d231",
          page: Npage,
        },
      });
    },
  },
};
</script>

<style lang="scss" scoped>
h1{
  margin: 10px 20px;
  text-align: left;
  text-shadow: 2px 2px 3px red;
}
</style>
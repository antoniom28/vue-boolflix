<template>
  <ul id="home">
    <FilmCards v-for="(film, index) in ratedFilm" :key="index" :films="film" />

    <div class="full-w load-more">
      <span @click="loadMore()" >
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
      startPage: 1,
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
    loadMore(){
      console.log('load');
      this.page++;
      this.getRatedFilm();
    },
    async getRatedFilm() {
      let response = await this.makeAxiosCall(
        `https://api.themoviedb.org/3/movie/popular`, this.page
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
ul {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: flex-start;
}

.load-more{
  font-size: 1.5em;
  height: 50px;
  margin-top: 10px;

  span{
    cursor: pointer;
  }
}
</style>
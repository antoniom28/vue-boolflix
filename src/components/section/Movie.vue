<template>
  <ul v-if="getInputText != null" id="movie">
    <FilmCards
        v-for="(film, index) in filterFilm"
        :key="index"
        :films="film"
        :inputType="inputType"
    />
  </ul>
</template>

<script>
import FilmCards from "../section/FilmCards.vue";
import axios from "axios";

export default {
  name: "Movie",
  data() {
    return {
      inputFilm: [],
    };
  },
  components: {
    FilmCards,
  },
  props: {
      filterSelect : Number,
      inputText: String,
      inputType : String,
  },
  computed: {
      getInputText(){
          if(this.inputText != "" && this.inputText != null)
          this.getFilm();
          return this.inputText;
      },
      filterFilm: function () {
      if(this.getInputText == '' || this.getInputText == null)
        return;
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
      async getFilm() {
      this.inputFilm = [];
      let response = await this.makeAxiosCall(
          `https://api.themoviedb.org/3/search/movie`,this.inputText,1
        );
        this.inputFilm.push(...response.data.results);
    },
    makeAxiosCall(url, input, page) {
      console.log("call of axos from movie");
      return axios.get(url, {
        params: {
          api_key: "8de7c27ea07119ebc4c79cbfffb7d231",
          query: input,
          page: page,
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
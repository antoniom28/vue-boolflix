<template>
  <ul class="section-list" v-show="getInputText != null" id="movie">
    <FilmCards
      v-for="(film, index) in filterFilm"
      :key="index"
      :films="film"
      :inputType="inputType"
    />

    <FilterEmpty v-if="filterError" />

    <div v-else class="full-w load-more">
      <span 
        v-if="!lastPage"
        @click="loadMore()"
      >
        LOAD MORE
        <i class="fas fa-angle-double-down"></i>
      </span>
      <span v-else>
        Non ci sono altri Film corrispondenti alla tua ricerca!
      </span>
    </div>
  </ul>
</template>

<script>
import FilmCards from "../section/FilmCards.vue";
import FilterEmpty from "../common/FilterEmpty.vue";
import axios from "axios";

export default {
  name: "Movie",
  data() {
    return {
      inputFilm: [],
      filterError: false,
      page: 1,
      prevInputText: "",
      lastPage : false,
      totalPage : 2,
    };
  },
  components: {
    FilmCards,
    FilterEmpty,
  },
  props: {
    filterSelect: Number,
    inputText: String,
    inputType: String,
  },
  computed: {
    getInputText() {
      this.updateInputText();

      if (this.inputText != "" && this.inputText != null) 
        if (this.page == 1) 
          this.getFilm();
      return this.inputText;
    },
    filterFilm: function () {
      if (this.getInputText == "" || this.getInputText == null) 
        return;
      let film = [];
      if (this.filterSelect == 0) 
        this.filterError = false;
      if (this.filterSelect != "" && this.filterSelect) {
        for (let i = 0; i < this.inputFilm.length; i++)
          for (let j = 0; j < this.inputFilm[i].genre_ids.length; j++)
            if (this.filterSelect == this.inputFilm[i].genre_ids[j])
              film.push(this.inputFilm[i]);

        if (film.length == 0) 
          this.filterError = true;
        else 
          this.filterError = false;

        return film;
      } else 
          return this.inputFilm;
    },
  },
  methods: {
    updateInputText() {
      if (this.prevInputText != this.inputText) {
        this.prevInputText = this.inputText;
        this.page = 1;
      }
    },
    loadMore() {
      this.page++;
      this.getFilm();
    },
    async getFilm() {
      if (this.page == 1) 
        this.inputFilm = [];
      if(this.totalPage < this.page){
        this.lastPage = true;
        return;
      } else
        this.lastPage = false;
      let response = await this.makeAxiosCall(
        `https://api.themoviedb.org/3/search/movie`,
        this.inputText,
        this.page
      );
      this.totalPage = response.data.total_pages;
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
</style>
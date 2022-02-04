<template>
  <div v-if="getInput" class="select-genre">
    <span @click="showFilter">
      <i class="fas fa-filter"></i>
    </span>
    <select
      v-model="option"
      v-if="filterBox"
      @change="filter"
      name="filter-genre"
      id="filter-genre"
    >
      <option :value="0">All</option>
      <option 
      :value="opt.id" 
      v-for="(opt, index) in optionList" :key="index"
      >
        {{ opt.name }}
      </option>
    </select>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Select",
  props: {
    optionArr: Array,
    filterSelect: Number,
    inputType: String,
  },
  data() {
    return {
      option: "",
      filterBox: false,
      filterSlct: this.filterSelect,
      optionList: this.optionArr,
    };
  },
  computed: {
    getInput: function () {
      let value = null;
      if (this.inputType != "HOME" && this.inputType) {
        this.getGenre();
        value = this.inputType;
      }
      return value;
    },
  },
  methods: {
    async getGenre() {
      let input = this.inputType.toLowerCase();
      let response = await this.makeAxiosCall(
        `https://api.themoviedb.org/3/genre/${input}/list`
      );
      this.optionList = response.data.genres;
    },
    makeAxiosCall(url) {
      return axios.get(url, {
        params: {
          api_key: "8de7c27ea07119ebc4c79cbfffb7d231",
        },
      });
    },
    showFilter() {
      this.filterBox = !this.filterBox;
    },
    filter() {
      this.filterSlct = this.option; //deve fare l'emit
      this.$emit("getFilterSelect", this.filterSlct);
    },
  },
};
</script>

<style lang="scss" scoped>
.select-genre {
  width: 100%;
  padding-left: 10px;
  padding-top: 10px;

  .fa-filter {
    font-size: 30px;
    vertical-align: middle;
    cursor: pointer;
  }

  select {
    margin-left: 6px;
    border-radius: 10px;
    width: 150px;
  }
}
</style>
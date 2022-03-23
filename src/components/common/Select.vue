<template>
  <div v-if="getInput && change" class="select-genre">
    <span 
     @click="showFilter"
     :class="{'filter-focus' : filterBox}"
    >
      <i class="fas fa-filter"></i>
    </span>
    <div v-if="filterBox" class="div-check">
      <div 
        v-for="(opt, index) in optionList" 
        :key="index" 
        class="option-check">
        <input
          v-model="filterSlct"
          type="checkbox"
          :name="opt.name"
          :id="opt.id"
          :value="{id : opt.id , name : opt.name}"
        />
        {{ opt.name }}<br />
      </div>

    </div>
      <div class="button-filter" v-if="filterBox">
        <button @click="filter">FILTER</button>
      </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Select",
  props: {
    optionArr: Array,
    filterSelect: Array,
    inputType: String,
  },
  data() {
    return {
      option: "",
      filterBox: false,
      filterSlct: this.filterSelect,
      prevInputType: "",
      optionList: this.optionArr,
    };
  },
  computed: {
    change: {
      get(){
        if(this.prevInputType != this.inputType){
          this.filterSlct = [];
          this.filter();
        }
        this.prevInputType = this.inputType;
        return true;
      },
    },
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
      this.filterBox = false;
      console.log(this.filterSlct);
      let name= [];
      let id = [];
      this.filterSlct.forEach((item,index) => {
        name.push(item.name);
        id.push(item.id)
      });
      this.$emit("getFilterSelect", id, name);
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../../assets/style/partials/variables.scss";

.filter-focus{
  color: $text_color;
}

.select-genre {
  .fa-filter {
    margin-left: 10px;
    margin-top: 10px;
    font-size: 30px;
    vertical-align: middle;
    cursor: pointer;
  }

  .button-filter{
    margin-top: 10px;
    text-align: center;

    button{
      padding: 3px;
      font-size: 1em;
      font-weight: bold;

      &:hover{
        color: rgb(71, 71, 71);
      }
    }
  }

  .div-check{
    width: 80%;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    height: 220px;
    justify-content: center;
    align-items: flex-start;
  }

  @media screen and (min-width: 601px) {
    .div-check{
      height: 100px!important;
    }
  }

  select {
    margin-left: 6px;
    border-radius: 10px;
    width: 150px;
  }
}
</style>
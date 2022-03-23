<!-- CHIAMATO DA HEADER -->
<template>
  <div class="container-cerca">
    <div class="input-cerca">
    <span @click="search">
      <i class="fas fa-search"></i>
    </span>
      <input
      @keyup.enter="search"
      v-model="inputText"
      type="text"
      name=""
      id=""
    />
    </div>

    <div 
      @click="search"
      class="button"
    >
        SEARCH
    </div>

    <select 
      @change="changeLang" 
      v-model="langSelected" 
      name="lang" id="language"
    >
      <option 
        v-for="(lang,index) in language"
        :key="index"
        :value="lang"
      >
          {{lang}}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "Cerca",
  data() {
    return {
      inputText: "",
      prevInput: "", //evita di chiamare l'axios se spammo l'enter
      language: ['it','en','pt','de'],
      langSelected: "it",
      showLang: true,
    };
  },
  methods: {
    changeLang(){
          this.showLang = !this.showLang;
          this.prevInput = this.inputText;
          if(this.inputText != "" && this.inputText != null)
            this.$emit("searchFilm", this.inputText, this.langSelected);
    },
    search: function () {
      if (this.inputControl(this.inputText)) {
        if (this.prevInput != this.inputText) {
          this.prevInput = this.inputText;
          this.$emit("searchFilm", this.inputText, this.langSelected);
        }
      }
    },
    inputControl(input) {
      input = input.replace(/\s/g, "");
      if (input == "") {
        this.inputText = "";
        return false;
      }
      return true;
    },
  },
};
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';
.container-cerca{
    display: flex;
    align-items: center;
}

div.language , div.button{
  display: inline-block;
  color: white;
  background-color: $text_color;
  width: 39px;
  padding: 5px 0;
  border-radius: 3px;
  text-align: center;
  cursor: pointer;
}

div.button{
  margin: 0 10px;
  width:  unset;
  padding: 5px 5px;
}

select{
  background-color: red;
  padding: 5px 0;
  color: white;

  &:focus-visible{
    outline: unset;
  }
}

.input-cerca{
  background-color: white;
  border-radius: 20px;
  padding: 2px 5px;

  span{
    color:black;
    cursor: pointer;
  }
}
input {
  height: 25px;
  width: 150px;
  margin-left: 5px;
  font-size: 1em;
  border: none transparent;
  outline: none;
  border-radius: 20px;
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
</style>
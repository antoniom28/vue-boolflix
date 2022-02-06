<!-- CHIAMATO DA HEADER -->
<template>
  <div class="container-cerca">
    <input
      @keyup.enter="search"
      v-model="inputText"
      type="text"
      name=""
      id=""
    />

    <div 
      class="language"
      v-if="showLang"
      @click="showLang = !showLang"
    > 
      {{langSelected}} 
    </div>
    <select 
      v-else
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
      if (this.inputControl(this.inputText)) {
          this.prevInput = this.inputText;
          this.$emit("searchFilm", this.inputText, this.langSelected);
        }
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

input {
  height: 25px;
  width: 150px;
  font-size: 1em;
}
div.language{
  display: inline-block;
  color: white;
  background-color: $text_color;
  width: 39px;
  padding: 3px 0;
  margin: 0 10px;
  border-radius: 3px;
  text-align: center;
  cursor: pointer;
}
select{
  margin: 0 10px;
}
</style>
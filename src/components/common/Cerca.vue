<template>
    <div class="container-cerca">
        <input 
        @keyup.enter="search" 
        v-model="inputText" 
        type="text" name="" id=""
        >
    </div>
</template>

<script>
export default {
    name: "Cerca",
    data(){
        return{
            inputText: "",
            prevInput: "",
        }
    },
    methods: {
      search: function(){
        if(this.inputControl(this.inputText)){
            if(this.prevInput != this.inputText){
                this.prevInput = this.inputText;
                this.$emit('searchFilm',this.inputText);
            }
        }
      },
      inputControl(input){
          input = input.replace(/\s/g, '');
          if(input == ''){
            this.inputText = '';
            return false;
            }
          return true;
      },
    },
}
</script>

<style lang="scss" scoped>
input{
    height: 25px;
    font-size: 1em;
}
</style>
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
      //inizia la "ricerca", controlla l'input se è valido e controlla
      //se è lo stesso che abbiamo già inserito
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
          //console.log('controll input : ',input);
          if(input == ''){
            //console.log('NON VA BENE: ',input);
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
<template>
    <div class="container-cerca">
        <input v-model="inputText" type="text" name="" id="">
        <button @click="search" >Cerca</button>
    </div>
</template>

<script>
export default {
    name: "Cerca",
    data(){
        return{
            inputText: "",
        }
    },
    methods: {
      search: function(){
        if(this.inputControl(this.inputText)){
            console.log('faccio l emit: ',this.inputText);
            this.$emit('searchFilm',this.inputText);
            this.inputText = '';
        }
      },
      inputControl(input){
          input = input.replace(/\s/g, '');
          console.log('controll input : ',input);
          if(input == ''){
            console.log('NON VA BENE: ',input);
            this.inputText = '';
            return false;
            }
          return true;
      },
    },
}
</script>

<style lang="scss" scoped>

</style>
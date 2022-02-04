<!-- CHIAMATO DA MAIN -->
<template>
  <li 
    :class="homePage"
    @mouseenter="showFace(false)" 
    @mouseleave="showFace(true)"
    >
  
      <FrontFace 
      v-if="mainFace"
      :films="films" />
    
      <BackFace 
        v-if="!details"
        @showDetails="showDetails"
        :films="films" 
      />

      <DetailsFace 
        v-if="details"
        @showDetails="showDetails"
        :id="idFilm"
        :inputType="inputType"
      />
  </li>
</template>

<script>
import FrontFace from "./FrontFace.vue";
import BackFace from "./BackFace.vue";
import DetailsFace from "./DetailsFace.vue";

export default {
  name: "ListaFilm",
  data(){
    return{
      details : false,
      mainFace : true,
      idFilm : null,
      type : null,
    }
  },
  components: {
    FrontFace,
    BackFace,
    DetailsFace,
  },
  props: {
    films: Object,
    inputType: String,
    filterSelect : String,
    homePage : String,
  },
  methods: {
    showDetails(id){
      //id è -1 se si torna indietro da DetailsFace
      this.details = !this.details;
      this.idFilm = id;
    },
    showFace(show){
      if(show)
        this.details = false;
      this.mainFace = show;
    },
  },
};
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';

li{
  position: relative;
  background-color: $bg_main_color;
  color: white;
  border: 2px ridge white;
  border-radius: 5px;
  list-style: none;
  margin: 10px;
  width: 280px;
  min-height: 400px;
} 


li.home-page{
  margin: 0;
  width: 320px;
  min-height: 440px;
}


</style>
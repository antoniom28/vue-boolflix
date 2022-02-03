<!-- CHIAMATO DA MAIN -->
<template>
  <li 
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
  },
  methods: {
    showDetails(id){
      //id è -1 se si torna indietro da DetailsFace
      this.details = !this.details;
      this.idFilm = id;
      //devo aggiungere il type
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

[class*="-face"] {
    width: 94%;
    height: 94%;
    position: absolute;
    top: 3%;
    left: 3%;
}

li {
  background-color: $bg_main_color;
  color: white;
  border: 2px ridge white;
  border-radius: 5px;
  list-style: none;
  margin: 10px;
  width: 230px;
  height: 342px;
  position: relative;
}
 
</style>
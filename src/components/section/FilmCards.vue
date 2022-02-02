<template>
  <li>
    <FrontFace :films="films" />
    <BackFace :films="films" />    
  </li>
</template>

<script>
import FrontFace from "./FrontFace.vue";
import BackFace from "./BackFace.vue";

export default {
  name: "ListaFilm",
  components: {
    FrontFace,
    BackFace,
  },
  props: {
    films: Object,
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
<!-- CHIAMATO DA FILMCARDS -->
<template>
    <div class="front-face">
      <img
        v-if="films.poster_path != null"
        :src="'https://image.tmdb.org/t/p/w500/' + films.poster_path"
        :alt="films.poster_path"
      />

      <div class="no-img" v-else>
        <h1>{{films.title}}</h1>
      </div>
     
    </div>
</template>

<script>
export default {
    name:"FrontFace",
    props: {
        films: Object,
    },
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';

.front-face{
    z-index: 999;
    background-color: $bg_main_color;

    img{
        width: 100%;
        height: 100%;
        box-shadow: 0 0 5px 1px whitesmoke;
    }

    .image-null{
      height: unset;
    }
}

.no-img{
  text-align: center;
  padding-top: 40px;
}
</style>
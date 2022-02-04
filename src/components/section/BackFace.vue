<!-- CHIAMATO DA FILMCARDS -->
<template>
    <div class="back-face">
      <div>
        <h5>Titolo Originale : &nbsp; </h5>
        <span>{{ getOriginalTitle(films) }}</span>
      </div>

      <div>
        <h5>Titolo : &nbsp; </h5>
        <span>{{ getTitle(films) }}</span>
      </div>

      <Flag :films="films"/>

      <div class="vote">
        <h5>Voto : &nbsp;</h5>
        <span 
          v-for="(star,index) in voteAverage(films.vote_average)" 
          :key="index"
        >
          <i class="fas fa-star"></i>
        </span>
      </div>

      <div class="overview">
          <h5>overview : &nbsp;</h5>
          <span>{{ films.overview }}</span>
      </div>

      <p class="see-details" @click="showDetails(films.id)">
        SEE DETAILS
      </p>

    </div>
</template>

<script>
import Flag from "./../common/Flag.vue";

export default {
    name:"BackFace",
    props: {
        films: Object,
    },
    components: {
        Flag,
    },
    methods: {
    showDetails(id){
      this.$emit('showDetails',id);
    },
    getOriginalTitle(film){
        if(film.original_title)
            return film.original_title;
        else if(film.original_name)
            return film.original_name;
    },
    getTitle(film){
        if(film.title)
            return film.title;
        else if(film.name)
            return film.name;
    },
    voteAverage(vote) {
      vote /= 2;
      vote = Math.ceil(vote);
      return vote;
    },
  },
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';

.see-details{
  cursor: pointer;
  position: absolute;
  bottom: 0;
  left: 10px;

  &:hover{
    color: $text_color;
  }
}

.back-face{
    padding: 10px;
    overflow: hidden;

    .overview{
         display: -webkit-box;
        -webkit-line-clamp: 7;
        -webkit-box-orient: vertical;  
        overflow: hidden;
    }
}
</style>
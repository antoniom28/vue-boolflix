<template>
  <li>
    <div class="front-face">
      <img
        v-if="films.poster_path != null"
        :src="'https://image.tmdb.org/t/p/w342/' + films.poster_path"
        :alt="films.poster_path"
      />
      <img
        class="image-null"
        v-else
        src="../../assets/img/image_null.jpg"
        alt=""
      />
    </div>

    <div class="back-face">
      <div v-if="films.original_title">
        <h5>Titolo Originale : &nbsp; </h5>
        <span>{{ films.original_title }}</span>
      </div>

      <div v-else>
        <h5>Titolo Originale : &nbsp; </h5>
        <span>{{ films.original_name }}</span>
      </div>

      <div v-if="films.title">
        <h5>Titolo :&nbsp; </h5>
        <span>{{ films.title }}</span>
      </div>

      <div v-else>
          <h5>Titolo :&nbsp; </h5>
          <span>{{ films.name }}</span>
        </div>


      <img class="lang" :src="putFlag(films.original_language)" alt="" />

      <div class="vote">
        <h5>Voto : &nbsp;</h5>
        <span v-for="star in voteAverage(films.vote_average)" :key="star">
          <i class="fas fa-star"></i>
        </span>
      </div>

      <div class="overview">
          <h5>overview : &nbsp;</h5>
          <span>{{ films.overview }}</span>
      </div>
    </div>
  </li>
</template>

<script>
export default {
  name: "ListaFilm",
  props: {
    films: Object,
  },
  methods: {
    voteAverage(vote) {
      vote /= 2;
      vote = Math.ceil(vote);
      return vote;
    },
    putFlag(lang) {
      let langArr = ["it", "en", "es"];
      let error = false;
      for (let i = 0; i < langArr.length; i++) {
        if (lang != langArr[i]) error = true;
        else {
          error = false;
          break;
        }
      }
      if (error) lang = "undefined";
      let flag = require(`../../assets/img/flag_${lang}.png`);

      return flag;
    },
  },
};
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';
h5{
    display: inline-block;
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

  [class*="-face"] {
    width: 94%;
    height: 94%;
    position: absolute;
    top: 3%;
    left: 3%;
  }
}

.front-face{
    z-index: 999;
    background-color: $bg_main_color;
    transition: opacity 0.3s linear;

    img{
        width: 100%;
        box-shadow: 0 0 5px 1px whitesmoke;
    }

    &:hover{
        opacity: 0;
    }
}

.back-face{
    padding: 10px;
    height: 200px;
    overflow: hidden;

    .overview{
         display: -webkit-box;
        -webkit-line-clamp: 10;
        -webkit-box-orient: vertical;  
        overflow: hidden;
    }
}

img.lang {
  width: 40px;
}

.fa-star {
  color: rgb(202, 172, 0);
  margin: 0 2px;
  border-radius: 20px;
  font-size: 1.5em;
}
</style>
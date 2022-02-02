<template>
    <div class="flag">
        <img class="lang" :src="putFlag(films.original_language)" alt="" />
    </div>
</template>

<script>
export default {
    name: 'Footer',
    props: {
        films: Object,
    },
    methods: {
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
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';

</style>
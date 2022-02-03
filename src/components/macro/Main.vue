<template>
    <main class="container">
        <ul>
            <FilmCards 
                v-for="(film,index) in inputFilm"
                :key="index"
                :films="film"
            />
        </ul>
    </main>
</template>

<script>
import FilmCards from '../section/FilmCards.vue'

export default {
    name: 'Main',
    components: {
        FilmCards,
    },
    props: {
        inputFilm : Array,
    },
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';
main{
    background-color: $bg_sec_color;
    min-height: calc(100vh - 60px);
}

ul{
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
    align-items: flex-start;
}
</style>
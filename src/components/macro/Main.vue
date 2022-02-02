<template>
    <main class="container">
        <ul>
            <ListaFilm 
                v-for="(film,index) in inputFilm"
                :key="index"
                :films="film"
            />
        </ul>
    </main>
</template>

<script>
import ListaFilm from '../section/ListaFilm.vue'

export default {
    name: 'Main',
    components: {
        ListaFilm,
    },
    props: {
        inputFilm : Array,
    },
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';

</style>
<template>
    <main class="container">
        <Cerca @searchFilm="getFilm" />
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
import axios from 'axios';
import ListaFilm from '../section/ListaFilm.vue'
import Cerca from '../common/Cerca.vue'

export default {
    name: 'Main',
    data(){
        return{
            inputFilm: [],
        }
    },
    components: {
        ListaFilm,
        Cerca,
    },
    created: function() {
        //this.getFilm();
    },
    methods: {
        getFilm(input){
            axios.get('https://api.themoviedb.org/3/search/movie', {
                params: {
                api_key: '8de7c27ea07119ebc4c79cbfffb7d231',
                query : input,
                }
            })
            .then((response) => {
                console.log(response.data.results);
                this.inputFilm = response.data.results;
            })
            .catch(function (error) {
                console.log(error);
            })
            .then(function () {
                // always executed
            });  
        },
    },
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';

</style>
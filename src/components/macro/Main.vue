<template>
    <main class="container">
        <Cerca @searchFilm="get" />
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
            urlType: ['movie','tv'],
        }
    },
    components: {
        ListaFilm,
        Cerca,
    },
    methods: {
        async get( input ){
            this.inputFilm = [],
            this.type = [],
            console.log( input );
            for(let i=0; i<this.urlType.length; i++){
                let response = await this.makeAxiosCall( `https://api.themoviedb.org/3/search/${this.urlType[i]}`, input )
                this.inputFilm.push(...response.data.results); 
            }
        },
        makeAxiosCall( url , input) {
            return axios.get( url , {
                params: {
                    api_key: '8de7c27ea07119ebc4c79cbfffb7d231',
                    query : input,
                }
            });
        },
    },
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';

</style>
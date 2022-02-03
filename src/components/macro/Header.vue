<template>
    <header class="container-header">
        <h2>BOOLFLIX</h2>
        <Cerca @searchFilm="get" />
    </header>
</template>

<script>
import axios from 'axios';
import Cerca from '../common/Cerca.vue';

export default {
    name: 'Header',
    data(){
        return{
            inputFilm: [],
            urlType: ['movie','tv'],
        }
    },
    components: {
        Cerca,
    },
    methods: {
        async get( input ){
            this.inputFilm = [];
            for(let i=0; i<this.urlType.length; i++){
                let response = await this.makeAxiosCall( `https://api.themoviedb.org/3/search/${this.urlType[i]}`, input )
                this.inputFilm.push(...response.data.results); 
                this.$emit('loadFilm',this.inputFilm);
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
header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: $bg_main_color;
    height: 60px;
    padding: 20px 25px 10px 25px;
    color: $text_color;
}
</style>
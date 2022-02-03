<template>
    <main class="container">
        <ul>
            <h2 v-if="getInput" class="full-w">
                Ricerca per : {{getInput}} 
                <i class="fas fa-filter"></i>
                <select v-model="option" 
                @change="filter"
                name="filter-genre" id="filter-genre">
                    <option 
                        :value="opt.name"
                        v-for="(opt,index) in optionArr"
                        :key="index"
                    >
                        {{opt.name}}
                    </option>
                </select>
            </h2>

            <FilmCards 
                v-for="(film,index) in inputFilm"
                :key="index"
                :films="film"
                :inputType="inputType"
            />
        </ul>
    </main>
</template>

<script>
import FilmCards from '../section/FilmCards.vue'
import axios from 'axios';

export default {
    name: 'Main',
    data(){
        return{
            option: "",
            optionArr : [],
        }
    },
    components: {
        FilmCards,
    },
    props: {
        inputFilm : Array,
        inputType : String,
    },
    computed: {
        getInput: function(){
            let value = null;
            if(this.inputType != 'HOME' && this.inputType){
                this.getGenre();
                value = this.inputType;
            }
            return value;
        }
    },
    methods: {
        filter(){
            console.log(this.option);
        },
        async getGenre(){
            let input = this.inputType.toLowerCase();
            let response = await this.makeAxiosCall( `https://api.themoviedb.org/3/genre/${input}/list`)
            this.optionArr = response.data.genres;
        },
        makeAxiosCall( url ) {
            return axios.get( url , {
                params: {
                    api_key: '8de7c27ea07119ebc4c79cbfffb7d231',
                }
            });
        },
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
    justify-content: center;
    align-items: flex-start;
}

.full-w{
    width: 100%;
    margin-top: 5px;
    text-align: center;
    color: white;
}
</style>
<template>
    <main class="container">
        <ul>
            <div v-if="getInput" class="select-genre">
                <span @click="showFilter"><i class="fas fa-filter"></i></span>
                <select v-model="option" v-if="filterBox"
                @change="filter"
                name="filter-genre" id="filter-genre">
                    <option value="">
                        All
                    </option>
                    <option 
                        :value="opt.id"
                        v-for="(opt,index) in optionArr"
                        :key="index"
                    >
                        {{opt.name}}
                    </option>
                </select>
            </div>

            <h2 v-if="getInput" class="full-w">
                Ricerca per : {{getInput}} 
            </h2>

            <FilmCards 
                v-for="(film,index) in filterFilm"
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
            filterSelect : "",
            filterBox : false,
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
        },
        filterFilm: function(){            
            let film = [];
            if(this.filterSelect != '' && this.filterSelect){
            for(let i=0; i<this.inputFilm.length; i++){
                for(let j=0; j<this.inputFilm[i].genre_ids.length; j++){
                    if(this.filterSelect == this.inputFilm[i].genre_ids[j])
                        film.push(this.inputFilm[i]);
                }
            }
            //console.log('filtrati',film);
            return film;
            } else
                return this.inputFilm;
        },
    },
    methods: {
        showFilter(){
            console.log('fi');
            this.filterBox = !this.filterBox;
        },
        filter(){
            this.filterSelect = this.option;
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

.select-genre{
    width: 100%;
    padding-left: 10px;
    padding-top: 10px;

    .fa-filter{
        font-size: 30px;
        vertical-align: middle;
        cursor: pointer;
    }

    select{
        margin-left: 6px;
        border-radius: 10px;
        width: 150px;
    }
}
</style>
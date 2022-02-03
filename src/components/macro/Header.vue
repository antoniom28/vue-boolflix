<template>
    <header class="container-header">
        <div>
            <h2>BOOLFLIX</h2>
            <p class="option home" @click="getInputType('home')">Home</p>
            <p class="option movie" @click="getInputType('movie')">Film</p>
            <p class="option tv" @click="getInputType('tv')">Serie TV</p>
        </div>
        <Cerca v-if="showSearch" @searchFilm="get" />
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
            page : 2,
            inputType : 'home', //da mettere topRated
            prevInput : null,
            showSearch : false,
        }
    },
    components: {
        Cerca,
    },
    methods: {
        noFocusOption(focus){
            for(let i=0; i<focus.length; i++)
                focus[i].style.color="grey";
            if(this.prevInput){
                this.get(this.prevInput,this.prevInput);
                }
        },
        getInputType(type){
            //la parte home è da modificare
            //in home, al posto di movie ci sarà la categoria topRated
            this.inputType = type;
            if(type != 'home')
                this.showSearch = true;
            else
                this.showSearch = false;
            this.noFocusOption(this.$el.querySelectorAll(`.option`));
            this.$el.querySelector(`.option.${type}`).style.color="white";
        },
        async get( input, prevInput ){
            this.prevInput = prevInput;
            this.inputFilm = [];
            if(this.inputType == 'home'){
                this.$emit('loadFilmApp',this.inputFilm,this.inputType);
                return;
            }
            let response;
            for(let i=0; i<this.page; i++){
                response = await this.makeAxiosCall( `https://api.themoviedb.org/3/search/${this.inputType}`, input , i + 1)
                this.inputFilm.push(...response.data.results); 
                this.$emit('loadFilmApp',this.inputFilm,this.inputType);
            }
        },
        makeAxiosCall( url , input, page) {
            return axios.get( url , {
                params: {
                    api_key: '8de7c27ea07119ebc4c79cbfffb7d231',
                    query : input,
                    page : page,
                }
            });
        },
    },
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';
h2,p{
    display: inline-block;
}

.option{
    color: grey;
}

.home{
    color: white;
}

p{
    margin: 0 15px;
    cursor: pointer;
}

header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: $bg_main_color;
    height: 60px;
    padding: 20px 25px 10px 25px;

    h2{
        color: $text_color;
    }
}
</style>
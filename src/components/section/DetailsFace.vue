<!-- CHIAMATO DA FILMCARDS -->
<template>
    <div class="details-face">
        <div @click="showDetails"> 
            <i class="fas fa-long-arrow-alt-left"></i> 
        </div>
        <h4>CAST : </h4>
        <span 
            v-for="(element,index) in info"
            :key="'a' + index"
        >
            {{ element.name }}
        </span>

        <h4>GENERI : </h4>
        <span 
            v-for="(genre,index) in genresInfo"
            :key="'b' + index"
        >
            {{ genre.name }}
        </span>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "DetailsFace",
    data(){
        return{
            info : [],
            genresInfo : [],
            input : null,
        }
    },
    props: {
        id : Number,
        inputType: String,
    },
    created: function(){
        this,this.input = this.inputType.toLowerCase();
        this.getInfo();
        this.getGenres();
    },
    methods: {
        showDetails(){
            this.$emit('showDetails',-1);
        },
        async getInfo(){
            let response = await this.makeAxiosCall( `https://api.themoviedb.org/3/${this.input}/${this.id}/credits`);
            let cast = response.data.cast;
            for(let i=0; i<5 && i<cast.length; i++)
                this.info.push(cast[i]);
        },
        async getGenres(){
            let response = await this.makeAxiosCall( `https://api.themoviedb.org/3/${this.input}/${this.id}`);
            let genres = response.data.genres;
            for(let i=0; i<5 && i<genres.length; i++)
                this.genresInfo.push(genres[i]);
        },
        makeAxiosCall( url) {
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
.fa-long-arrow-alt-left{
        transform: scale(1.4);

    &:hover{
        transform: scale(1.7);
        color: red;
        cursor: pointer;
    }
}

span{
    display: block;
}

.details-face{
    padding: 10px;
}

h4{
    margin-top: 10px;
    margin-bottom: 5px;
}
</style>
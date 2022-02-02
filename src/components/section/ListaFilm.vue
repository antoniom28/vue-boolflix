<template>
    <li>
        <img
            v-if="films.backdrop_path != null"
            :src="'https://image.tmdb.org/t/p/w300/' + films.backdrop_path" 
            :alt="films.backdrop_path"
        >
        <img class="img-null" v-else src="../../assets/img/image_null.jpg" alt="">

        <h2 
            v-if="films.original_title
        ">
            FILM <br>
            {{films.original_title}}
        </h2>
        <h2 v-else >
            SERIES <br>
            {{films.original_name}}
        </h2>

        <h3  
            v-if="films.original_title != ''
        ">
            {{films.title}}
        </h3>
        <h3 v-else>{{films.name}}</h3>

        <img class="lang" :src="putFlag(films.original_language)" alt="">

        <div class="vote">
            <span 
                v-for="(star) in voteAverage(films.vote_average)"
                :key="star"
            >
                <i class="fas fa-star"></i>
            </span>
        </div>
    </li>
</template>

<script>
export default {
    name: "ListaFilm",
    props: {
        films : Object,
    },
    methods: {
        voteAverage(vote){
            console.log(vote,'prima');
            vote /= 2;
            vote = Math.ceil(vote);
            console.log(vote);
            return vote;
        },
        putFlag(lang){
            //console.log(lang);
            let langArr = ['it','en','es'];
            let error = false;
            for(let i=0; i<langArr.length; i++){
                if(lang != langArr[i])
                    error = true;
                else{
                    error = false;
                    break;
                }
            }
            if(error)
                lang = 'undefined';
            let flag = require(`../../assets/img/flag_${lang}.png`);

            return flag;
        }
    },
}
</script>

<style lang="scss" scoped>
li{
    border: 1px solid black;
    list-style: none;
    margin: 10px;
}

img.lang{
    width: 40px;
}

.img-null{
    width: 300px;
}

.fa-star{
    color: rgb(202, 172, 0);
    box-shadow: 
        0 0 5px 0px gold,
        inset 0 0 10px 0 gold,
    ;
    margin: 0 2px;
    border-radius: 20px;
}
</style>
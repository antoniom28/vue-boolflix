<template>
    <li>
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

        <img :src="putFlag(films.original_language)" alt="">

        <div class="vote">
            {{films.vote_average}}
            {{films.vote_count}}
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

img{
    width: 40px;
}

</style>
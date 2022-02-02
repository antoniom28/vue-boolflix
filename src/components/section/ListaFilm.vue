<template>
    <li>
        <h2>{{films.title}}</h2>
        <h3>{{films.original_title}}</h3>
        <span>
            <img :src="putFlag(films.original_language)" alt="">
        </span>
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
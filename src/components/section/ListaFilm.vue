<template>
    <li>
        <h2>{{films.title}}</h2>
        <h3>{{films.original_title}}</h3>
        <span>{{films.original_language}}</span>
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
}
</script>

<style lang="scss" scoped>
li{
    border: 1px solid black;
    list-style: none;
    margin: 10px;
}

</style>
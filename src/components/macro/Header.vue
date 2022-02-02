<template>
    <header class="container">
        <div class="row">
            <div class="col">
                <h1 class="text-center my-5">
                    {{msg}}
                </h1>
            </div>
        </div>
    </header>
</template>

<script>
export default {
    name: 'Header',
    props: {
        msg : String,
    },
}
</script>

<style lang="scss" scoped>
@import '../../assets/style/partials/variables.scss';

</style>
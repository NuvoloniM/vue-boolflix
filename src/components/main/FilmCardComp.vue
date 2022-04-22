<template>
    <div class="card" style="width: 18rem;">
        <img :src="`${imgSize}${image}`" class="card-img-top" alt="...">
        <!-- <div class="card-body">
            <h5 class="card-title"> {{title}} </h5>
            <p class="card-text"> {{overview}} </p>
            <a href="#" class="btn btn-primary">Go somewhere</a>
        </div> -->
    </div>
</template>

<script>
export default {
    name: 'FilmCardComp',
    data(){
        return {
            imgSize: 'https://image.tmdb.org/t/p/w500',
        }
    },
    props: {
        title: String,
        overview: String,
        image: String,
    }
}
</script>

<style lang="scss" scoped>

</style>
<template>
    <div class="card col-2 my-2 p-0">
        <img :src="`${imgSize}${image}`" class="img-fluid" alt="...">
        <!-- <div class="card-body">
            <h5 class="card-title"> {{title}} </h5>
            <p class="card-text"> {{overview}} </p>
            <a href="#" class="btn btn-primary">Go somewhere</a>
        </div> -->
    </div>
</template>

<script>
export default {
    name: 'TelefilmCardComp',
    data(){
        return {
            imgSize: 'https://image.tmdb.org/t/p/w500',
        }
    },
    props: {
        name: String,
        overview: String,
        image: String,
    }
}
</script>

<style lang="scss" scoped>
    .card{
        border-color: rgb(200, 187, 187);
    }
</style>
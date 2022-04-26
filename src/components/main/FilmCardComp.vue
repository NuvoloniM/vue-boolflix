<template>
    <div class="card col-2 my-2 p-0">
        <img :src="`${imgSize}${image}`" class="img-fluid" alt="...">
        <!-- <div class="card-body">
            <h5 class="card-title"> {{title}} </h5>
            <p class="card-text"> {{overview}} </p>
            <a href="#" class="btn btn-primary">Go somewhere</a>
        </div> -->
        <img :src="language" class="test" alt="">
    </div>
</template>

<script>
export default {
    name: 'FilmCardComp',
    data(){
        return {
            imgSize: 'https://image.tmdb.org/t/p/w500',
            language: this.chooseFlag(this.flag),
        }
    },
    props: {
        title: String,
        overview: String,
        image: String,
        flag: String,
    },
    methods: {
        chooseFlag(flag) {
            if (flag == 'en') {
                console.log('inglese')
                return this.language= require("../../assets/img/icons8-gran-bretagna-48.png")
            } else if (flag == 'fr') {
                console.log('francese')
                return this.language= require("../../assets/img/icons8-francia-48.png") 
            } else if( flag == "it"){
                console.log('italiano')
                return this.language= require("../../assets/img/icons8-italia-48.png")
            } else {
                console.log('nessuna bandiera')
                return this.language= require ("../../assets/img/pngegg.png");
            }
        }
    }
}
</script>

<style lang="scss" scoped>
    .card{
        border-color: rgb(200, 187, 187);
        background-color: rgb(200, 187, 187);
    }
    .test{
        width: 50px;
        height: 50px;
    }
</style>
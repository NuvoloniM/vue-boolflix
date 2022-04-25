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
        chooseFlag(lang) {
            switch (lang) {
                case 'en':
                    console.log('inglese')
                    return this.language= require("../../assets/img/5a376b7ab7a2c2.4464593815135814347522.png")
                case 'fra':
                    console.log('francese')
                    return this.language= require("../../assets/img/kisspng-flag-of-france-flag-of-the-united-kingdom-french-5af2dbc55b5244.0446619815258654133741.png")
            
                case 'ita':
                    console.log('italiano')
                    return this.language= require("../../assets/img/kisspng-flag-of-italy-flag-of-the-united-states-national-f-italy-flag-5abf21d71305e4.6793026015224754790779.png")
            
                default:
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
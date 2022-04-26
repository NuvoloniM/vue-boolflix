<template>
    <div class="card col-2 my-2 p-0">
        <img :src="`${imgSize}${image}`" class="img-fluid" alt="...">
        <div class="card-body">
            <h5 class="card-title"> {{title}} </h5>
            <h6 class="card-title"> {{originalTitle}} </h6>
            <img :src="language" class="test" alt="">
            <p class="card-text"> {{overview}} </p>
            <p class="card-text">
                <ul class="d-flex align-items-center justify-content-between">
                    <li 
                    v-for="(element,index) in starArray" 
                    :key="index"
                    >
                    <img v-if="element == 'y'" src="../../assets/img/icons8-stella-riempita-16.png" alt="">
                    <img v-else src="../../assets/img/icons8-stella-50.png" alt="">
                    </li>
                </ul>
            </p>
            <p class="card-text">  {{vote}} </p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'FilmCardComp',
    data(){
        return {
            imgSize: 'https://image.tmdb.org/t/p/w500',
            language: this.chooseFlag(this.flag),
            starArray: [],
        }
    },
    props: {
        title: String,
        originalTitle: String,
        overview: String,
        image: String,
        flag: String,
        vote: Number,
    },
    created() {
        this.voteStar();
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
        },
        voteStar() {
            for (let i = 1; i <= 5; i++) {
                let media = Math.floor((this.vote / 2))
                if (media >= i){
                    this.starArray.push('y');
                    console.log(this.starArray);           
                } else {
                    this.starArray.push('n');
                    console.log(this.starArray);   
                }
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

    ul {
        list-style-type: none;
        padding: 0;

        img {
            width: 30px;
            height: 30px;
        }
    }
</style>
<template>
    <div class="flip-card col-2 my-2 p-2">
        <div class="flip-card-inner">
            <div class="flip-card-front">
                <img :src="`${imgSize}${image}`" alt="Film Poster" class="">
            </div>
            <div class="flip-card-back overflow-auto">
                <h5 class="card-title">{{title}}</h5> 
                <h6 class="card-title"> {{originalTitle}} </h6>
                <p class="card-text mb-1">
                    <ul v-if="cast.length > 0" class="d-flex flex-wrap align-items-center justify-content-start mb-1">
                        <li>Cast: </li>
                        <li v-for="element in cast" :key="element.cast_id" class="cast_text"> - {{element.name}}  </li>
                    </ul>
                    <ul v-if="genres.length > 0" class="d-flex flex-wrap align-items-center justify-content-start mb-1">
                        <li>Genres: </li>
                        <li v-for="element in genres" :key="element.id" class="cast_text"> - {{element.name}}  </li>
                    </ul>
                </p>
                <p class="card-text mb-1">
                    <ul class="d-flex align-items-center justify-content-center mb-1">
                        <li class="pe-2"> {{ vote/2 }} </li>
                        <li v-for="i in 5" :key="i">
                            <font-awesome-icon v-if="i <= voteStar()" icon="fa-solid fa-star" class="text-y" /> 
                            <font-awesome-icon v-else icon="fa-regular fa-star" /> 
                        </li>
                    </ul>
                </p>
                <img :src="language" class="test" alt="">
                <p class="fst-italic"> {{overview}} </p>
            </div>
        </div>
    </div>
</template>

<script>

import axios from 'axios';

export default {
    name: 'FilmCardComp',
    data(){
        return {
            imgSize: 'https://image.tmdb.org/t/p/w342',
            language: this.chooseFlag(this.flag),
            cast: [],
            genres: [],
        }
    },
    props: {
        title: String,
        originalTitle: String,
        overview: String,
        image: String,
        flag: String,
        vote: Number,
        idMovies: Number,
        personalKey: String,
    },
    created() {
        this.detailsMovie()
        
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
            return Math.floor((this.vote / 2))
        },
        detailsMovie() {
            axios.get( `https://api.themoviedb.org/3/movie/${this.idMovies}/credits?api_key=${this.personalKey}` )
                .then( (res) =>{
                    for (let i = 0; i < 5; i++) {
                        this.cast.push(res.data.cast[i])
                        console.log(this.cast)
                    }
                }
            )
            axios.get( `https://api.themoviedb.org/3/movie/${this.idMovies}?api_key=${this.personalKey}` )
                .then( (res) =>{
                    for (let i = 0; i < res.data.genres.length; i++) {
                        this.genres.push(res.data.genres[i])
                        console.log(this.genres)
                    }
                }
            )
        },
    }
}
</script>

<style lang="scss" scoped>
.text-y{
    color: yellow;
}
    // .card_test{
    //     border-color: rgb(200, 187, 187);
    //     background-color: rgb(200, 187, 187);
    .flip-card {
        background-color: transparent;
        height: 300px;
        // width: 300px; 
        perspective: 1000px;
    }

    .flip-card-inner {
        position: relative;
        width: 100%;
        height: 100%;
        text-align: center;
        transition: transform 0.6s;
        transform-style: preserve-3d;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
    }
    .flip-card:hover .flip-card-inner {
        transform: rotateY(-180deg);
    }

    .flip-card-front, .flip-card-back {
        position: absolute;
        width: 100%;
        height: 100%;
        backface-visibility: hidden;
    }

    .flip-card-front {
        background-color: #bbb;
        color: black;
        img {
            height: 100%;
            width: 100%;
        }
    }

    .flip-card-back {
        background-color: rgb(21, 1, 1);
        color: white;
        transform: rotateY(180deg);
    }
// }
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

        .cast_text{
            font-size: 0.7em;
            color: lightgray;
            font-style: italic;
            padding: 0;
        }
    }

</style>
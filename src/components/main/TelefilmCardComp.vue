<template>
    <div class="card_ col-2 my-2 p-0 flip-card">
        <div class="flip-card-inner">
             <div class="flip-card-front">
                <img :src="`${imgSize}${image }`" class="img-fluid" alt="...">
            </div>
            <div class="card-body flip-card-back">
                <h5 class="card-title"> {{name}} </h5>
                <h6 class="card-title"> {{originalName}} </h6>
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
                <p class="card-text"> {{vote}} </p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'TelefilmCardComp',
    data(){
        return {
            imgSize: 'https://image.tmdb.org/t/p/w500',
            language: this.chooseFlag(this.flag),
            starArray: [],
        }
    },
    props: {
        name: String,
        originalName: String,
        overview: String,
        image: String,
        flag: String,
        vote: Number,
    },
    created() {
        this.voteStar();
    },
    methods: {
        chooseFlag(lang) {
            if (lang == 'en') {
                console.log('inglese')
                return this.language= require("../../assets/img/icons8-gran-bretagna-48.png");
            } else if (lang == 'fr') {
                console.log('francese')
                return this.language= require("../../assets/img/icons8-francia-48.png"); 
            } else if( lang == "it"){
                console.log('italiano')
                return this.language= require("../../assets/img/icons8-italia-48.png");
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
    .card_{
        border-color: rgb(200, 187, 187);
        background-color: rgb(200, 187, 187);
//     .flip-card {
//         background-color: transparent;
//         height: 300px;
//         width: 300px;
//         perspective: 1000px;

//         .flip-card-inner {
//             position: relative;
//             width: 100%;
//             height: 100%;
//             text-align: center;
//             transition: transform 0.6s;
//             transform-style: preserve-3d;
//             box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
//         }

//     }
//     .flip-card:hover .flip-card-inner {
//         transform: rotateY(180deg);
//     }

//     .flip-card-front, .flip-card-back {
//         position: absolute;
//         width: 100%;
//         height: 100%;
//         backface-visibility: hidden;
//     }

//     .flip-card-front {
//         background-color: #bbb;
//         color: black;
//         img {
//             width: 300px;
//             height: 300px;
//         }
//     }

//     .flip-card-back {
//         background-color: #2980b9;
//         color: white;
//         transform: rotateY(180deg);
//     }
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
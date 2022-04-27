<template>
<div>
    <select 
    class="form-select d-inline-block w-25" 
    aria-label="Default select example" 
    v-model="selectedTvGenres"
    @click.prevent="$emit ( 'selectTvResult', selectedTvGenres)"
    >
        <option selected>Open this select a genres</option>
        <option v-for="element in allGenres" :key="element.id" :value="element.id"> {{element.name}} </option>
        <!-- <option value="1">One</option>
        <option value="2">Two</option>
        <option value="3">Three</option> -->
    </select>
</div>
</template>

<script>

import axios from 'axios'

export default {
    name: 'SelectComp',
    data(){
        return{
            allGenres: [],
            selectedTvGenres: '',
        }
    },
    props: {
        personalKey: String,
    },
    created(){
        this.getAllFilm()
    },
    methods: {
        getAllFilm() {
            axios.get( `https://api.themoviedb.org/3/genre/tv/list?api_key=${this.personalKey}&language=en-US` )
                .then( (res) =>{
                console.log(res.data.genres);
                for (let i = 0; i < res.data.genres.length; i++) {
                    this.allGenres.push(res.data.genres[i]);
                }
            })
        }
    }
}
</script>

<style lang="scss" scoped>

</style>
<template>
  <div>
    <header class="d-flex justify-content-between align-items-center p-2">
      <LogoComp/>
      <InputComp
      @inputResult="inputResultFunction"
      />
    </header>
    <main>
      <div class="row px-2 mx-0">
        <h2 v-if="this.filteredFilm.length > 0" class="ps-3 py-2">Film</h2>
        <SelectFilmComp
        v-if="this.filteredFilm.length > 0"
        :personalKey="personalKey"
        @selectFilmResult="selectFilmResultFunction"
        />
        <FilmCardComp
        :personalKey="personalKey"
        v-for="element in filterMovie()"
        :key="element.id"
        :originalTitle="element.original_title"
        :title="element.title"
        :overview="element.overview"
        :image="element.poster_path"
        :flag="element.original_language"
        :vote="element.vote_average"
        :idMovies="element.id"
        />
      </div>
      <div class="row px-2 mx-0">
        <h2 v-if="this.filteredTelefilm.length > 0" class="ps-3 py-2">Telefilm</h2>
        <SelectTelefilmComp
        v-if="this.filteredFilm.length > 0"
        :personalKey="personalKey"
        @selectTvResult="selectTvResultFunction"
        />
        <TelefilmCardComp
        :personalKey="personalKey"
        v-for="element in filterTelefilm()"
        :key="element.id"
        :name="element.name"
        :originalName="element.name"
        :overview="element.overview"
        :image="element.poster_path"
        :flag="element.original_language"
        :vote="element.vote_average"
        :idTelefilm="element.id"
        />
      </div>
    </main>
  </div>
</template>

<script>

import "bootstrap";
import axios from 'axios';
import LogoComp from "./components/header/LogoComp.vue";
import SelectFilmComp from "./components/main/SelectFilmComp.vue";
import SelectTelefilmComp from "./components/main/SelectTelefilmComp.vue";
import InputComp from "./components/header/InputComp.vue";
import FilmCardComp from "./components/main/FilmCardComp.vue";
import TelefilmCardComp from "./components/main/TelefilmCardComp.vue";

export default {
  name: 'App',
  data() {
    return{
      personalKey: 'ac7ccea2c466d848c3c9dc330aad7c80',
      filteredFilm: [],
      filteredTelefilm:[],
      selectedFilmGenres: '',
      selectedTvGenres: '',
    }
  },
  components: {
    LogoComp,
    InputComp,
    SelectFilmComp,
    SelectTelefilmComp,
    FilmCardComp,
    TelefilmCardComp,
  },
  created() {
  },
  methods: {
    inputResultFunction(testo){
      console.log(testo);
      axios.get( `https://api.themoviedb.org/3/search/movie?api_key=${this.personalKey}&language=it_IT&query=${testo}` )
        .then( (res) =>{
          console.log(res.data.results);
          this.filteredFilm = res.data.results;
        }
      )
      axios.get( `https://api.themoviedb.org/3/search/tv?api_key=${this.personalKey}&language=it_IT&query=${testo}` )
        .then( (res) =>{
          console.log(res.data.results);
          this.filteredTelefilm = res.data.results;
        }
      )
    },
    selectFilmResultFunction( testo ) {
      console.log(testo);
      this.selectedFilmGenres = testo;
    },
    selectTvResultFunction( testo ) {
      console.log(testo);
      this.selectedTvGenres = testo;
    },
    filterMovie(){
            if( this.selectedFilmGenres == ""){
                return this.filteredFilm;    
            } else {
                return this.filteredFilm.filter( (elem) => {
                    return elem.genre_ids.includes(this.selectedFilmGenres);
                } )
            }
    },
    filterTelefilm(){
            if( this.selectedTvGenres == ""){
                return this.filteredTelefilm;    
            } else {
                return this.filteredTelefilm.filter( (elem) => {
                    return elem.genre_ids.includes(this.selectedTvGenres);
                } )
            }
    }
  }
}
</script>

<style lang="scss">
@import "bootstrap/dist/css/bootstrap.min.css";

header {
  background-color: black;
  height: 86px;
}
main {
  height: calc( 100vh - 86px);
  background-color: rgb(200, 187, 187);
  overflow-y: auto;
}
</style>

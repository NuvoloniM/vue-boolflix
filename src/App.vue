<template>
  <div>
    <header class="d-flex justify-content-between align-items-center p-2">
      <LogoComp/>
      <InputComp
      @inputResult="inputResultFunction"
      />
    </header>
    <main>
      <div class="row">
        <h2 v-if="this.filteredFilm.length > 0" class="ps-3 py-2">Film</h2>
        <FilmCardComp
        :personalKey="personalKey"
        v-for="element in filteredFilm"
        :key="element.id"
        :title=element.original_title
        :overview="element.overview"
        :image="element.poster_path"
        :flag="element.original_language"
        />
      </div>
      <div class="row">
        <h2 v-if="this.filteredTelefilm.length > 0" class="ps-3 py-2">Telefilm</h2>
        <TelefilmCardComp
        v-for="element in filteredTelefilm"
        :key="element.id"
        :name="element.name"
        :overview="element.overview"
        :image="element.poster_path"
        :flag="element.original_language"
        />
      </div>
    </main>
  </div>
</template>

<script>

import "bootstrap";
import axios from 'axios';
import LogoComp from "./components/header/LogoComp.vue";
import InputComp from "./components/header/InputComp.vue";
import FilmCardComp from "./components/main/FilmCardComp.vue";
import TelefilmCardComp from "./components/main/TelefilmCardComp.vue";

export default {
  name: 'App',
  data() {
    return{
      personalKey: 'ac7ccea2c466d848c3c9dc330aad7c80',
      inputFilm: '',
      filteredFilm: [],
      inputTelefilm: '',
      filteredTelefilm:[],
    }
  },
  components: {
    LogoComp,
    InputComp,
    FilmCardComp,
    TelefilmCardComp,
  },
  created() {
  },
  methods: {
    inputResultFunction(testo){
      console.log(testo);
      this.inputFilm = testo;
      axios.get( `https://api.themoviedb.org/3/search/movie?api_key=${this.personalKey}&language=it_IT&query=${this.inputFilm}` )
        .then( (res) =>{
          console.log(res.data.results);
          this.filteredFilm = res.data.results;
        }
      )
      this.inputTelefilm = testo;
      axios.get( `https://api.themoviedb.org/3/search/tv?api_key=${this.personalKey}&language=it_IT&query=${this.inputTelefilm}` )
        .then( (res) =>{
          console.log(res.data.results);
          this.filteredTelefilm = res.data.results;
        }
      )
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

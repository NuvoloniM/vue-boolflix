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
        <FilmCardComp
        v-for="element in filteredFilm"
        :key="element.id"
        :title=element.original_title
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

export default {
  name: 'App',
  data() {
    return{
      inputFilm: '',
      filteredFilm: [],
    }
  },
  components: {
    LogoComp,
    InputComp,
    FilmCardComp,
  },
  created() {
  },
  methods: {
    inputResultFunction(testo){
      console.log(testo);
      this.inputFilm = testo;
      axios.get( `https://api.themoviedb.org/3/search/movie?api_key=ac7ccea2c466d848c3c9dc330aad7c80&query=${this.inputFilm}` )
        .then( (res) =>{
          console.log(res.data.results);
          this.filteredFilm = res.data.results;
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

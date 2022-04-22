<template>
  <div>
    <header class="d-flex justify-content-between align-items-center p-2">
      <LogoComp/>
      <InputComp
      @inputResult="inputResultFunction"
      />
    </header>
  </div>
</template>

<script>

import "bootstrap";
import axios from 'axios';
import LogoComp from "./components/header/LogoComp.vue";
import InputComp from "./components/header/InputComp.vue";

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
}
</style>

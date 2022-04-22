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
import LogoComp from "./components/header/LogoComp.vue";
import InputComp from "./components/header/InputComp.vue";

export default {
  name: 'App',
  data() {
    return{
      inputFilm: '',
    }
  },
  components: {
    LogoComp,
    InputComp,
  },
  methods: {
    inputResultFunction(testo){
      console.log(testo);
      this.inputFilm = testo;
      console.log(this.inputFilm);
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

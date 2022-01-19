<template>
  <div id="app">
    <Header @doSearch="search($event)"></Header>
    <Main :inputHeader="movieApi"></Main>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";

export default {
  name: "App",
  components: {
    Header,
    Main,
  },
  data(){
    return {
      movieApi: '',
    }
  },
  methods: {
    search(value) {
      this.movieApi = value;
    },
  }
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
</style>

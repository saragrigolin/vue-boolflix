<template>
  <div id="app">
    <Header @doSearch="search($event)"></Header>
    <Main :movieApi="movieApi"></Main>
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
      movieApi: {
        movies: null,
        tv: null,
      },
    }
  },
  methods: {
    search(value) {
      this.movieApi.movies = value.movies;
      this.movieApi.tv = value.tv;
    },
  }
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
@import '~mdb-ui-kit/css/mdb.min.css';
@import "./assets/scss/style.scss";
body {
  background-color: $bodyBackground;
}
</style>

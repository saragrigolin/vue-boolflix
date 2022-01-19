<template>
  <div id="app">
    <Header @doSearch="search($event)" :inputValue="text"></Header>
    <Main></Main>
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
      text: '',
      staticApi: "https://api.themoviedb.org/3/search/movie?api_key=4148b7accd7bd65952002b841924594e&query=",
    }
  },
  methods: {
    search(value) {
      this.text = this.staticApi + value;
    },
  }
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
</style>

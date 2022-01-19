<template>
	<header>
		<div class="search">
			<input id="search" v-model="inputText" type="text" name="search" @keyup.enter="getApi">
			<button class="btn btn-primary" type="submit" @click="getApi"> Cerca</button>
		</div>
	</header>
</template>

<script>
import axios from 'axios';

export default {
	name: "Header",
	data(){
		return {
			inputText: '',
			inputFinal: '',
			movies: [],
			originalApi: "https://api.themoviedb.org/3/search/movie?api_key=4148b7accd7bd65952002b841924594e&query="
		}
	},
	methods: {
		getApi() {
			this.inputFinal = this.inputText.replace(/\s/g, "+");
			console.log(this.inputFinal);
			axios.get(this.originalApi, {
				params: {
					query: this.inputFinal
				}
			})
			.then((result) => {
				this.movies = result.data.results;
				this.$emit('doSearch', this.movies);
			})
			.catch((error) => {
				console.log(error);
			})
		}
	}
}
</script>

<style lang="scss">

</style>
<template>
	<header class="my-3">
		<div class="search container">
			<input id="search" v-model="inputText" type="text" name="search" @keyup.enter="getSearch">
			<button class="btn btn-primary" type="submit" @click="getSearch"> Cerca</button>
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
			merged: {
				movies: [],
				tv: [],
			},
			query: 'https://api.themoviedb.org/3/search/',
			api_key: '4148b7accd7bd65952002b841924594e',
		}
	},
	created(){
	},
	methods: {
		getFilms() {
			const movie = 'movie';
			const parameters = {
				api_key: this.api_key,
				query: this.inputText,
			};
			axios.get(`${this.query}${movie}`, { params: parameters })
			.then((result) => {
				this.merged.movies = result.data.results;
			})
			.catch((error) => {
				console.log(error);
			})
		},
		getSerieTv(){
			const tv = 'tv';
			const parameters = {
				api_key: this.api_key,
				query: this.inputText,
			};
			axios.get(`${this.query}${tv}`, { params: parameters })
				.then((result) => {
					this.merged.tv = result.data.results;
				})
				.catch((error) => {
					console.log(error);
				});
		},
		getSearch(){
			this.getFilms();
			this.getSerieTv();
			setTimeout(() => {
				this.$emit('doSearch', this.merged);
			}, 500);	
		}
	}
}
</script>

<style lang="scss">
@import "../assets/scss/style.scss";

</style>
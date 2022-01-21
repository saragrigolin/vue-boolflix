<template>
	<header class="">
		<div class="container">
			<div class="row">
				<div class="col-12 d-flex justify-content-between">
					<div class="logo">
						<img src="../assets/netflix-logo.png" alt="">
					</div>
					<div class="d-flex align-items-center">
						<div class="search-container d-flex align-items-center">
							<input placeholder="Inserisci titolo" id="search" v-model="inputText" type="text" name="search" @keyup.enter="getSearch">
							<button class="my_btn btn btn-light ms-2" type="submit" @click="getSearch">Cerca</button>
						</div>
					</div>
				</div>
			</div>
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
header {
	background-color: $headerBackground;
	.logo {
		width: 20%;
		img {
		width: 100%;
	}
	}
	.search-container {
		height: 30%;
	}
	#search {
		outline: none;
		height: 100%;
		font-size: 0.9rem;
	}
	.my_btn {
		text-transform: none !important;
		font-size: 0.8rem;
		height: 100%;
		padding: 0 1em;
	}
}
</style>
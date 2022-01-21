<template>
	<main class="container mt-3">
    	<div v-if="inputHeader.movies.length > 0" class="row row-cols-5">
        	<Card v-for="(movie, index) in inputHeader.movies" :key="index+'movies'"
			:title="movie.title" 
			:original="movie.original_title" 
			:lang="movie.original_language"
			:vote="movie.vote_average"
			:poster="movie.poster_path"
			:plot="movie.overview"
			:image="`https://image.tmdb.org/t/p/w342${movie.poster_path}`">
			</Card>
		</div>
		<h2 v-else>Nessun film trovato</h2>
		<div v-if="inputHeader.tv.length > 0" class="row row-cols-5">
			<Card v-for="(serie, index) in inputHeader.tv" :key="index+'tv'"
			:title="serie.name" 
			:original="serie.original_name" 
			:lang="serie.original_language"
			:vote="serie.vote_average"
			:poster="serie.poster_path"
			:plot="serie.overview"
			:image="`https://image.tmdb.org/t/p/w342${serie.poster_path}`">
			</Card>
		</div>
		<h2 v-else>Nessuna serie TV trovata</h2>
	</main>
</template>

<script>
import Card from './Card.vue'

export default {
	name: "Main",
	props: ["inputHeader"],
	data(){
		return {

		}
	},
	components: {
		Card,
	}
}
</script>

<style lang="scss">
@import "../assets/scss/style.scss";
h2 {
	color: white;
}
</style>
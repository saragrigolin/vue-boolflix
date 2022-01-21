<template>
	<main class="container mt-3">
		<div v-if="movieApi.movies || movieApi.tv">
			<div v-show="movieApi.movies">
				<div v-if="movieApi.movies.length > 0" class="row row-cols-5">
					<Card v-for="(movie, index) in movieApi.movies" :key="index+'movies'"
					:title="movie.title" 
					:original="movie.original_title" 
					:lang="movie.original_language"
					:vote="movie.vote_average"
					:poster="movie.poster_path"
					:plot="movie.overview"
					:image="`https://image.tmdb.org/t/p/w342${movie.poster_path}`">
					</Card>
				</div>
				<h4 v-else>Nessun film trovato</h4>
			</div>
			<div v-show="movieApi.tv" class="mt-4">
				<div v-if="movieApi.tv.length > 0" class="row row-cols-5">
					<Card v-for="(serie, index) in movieApi.tv" :key="index+'tv'"
					:title="serie.name" 
					:original="serie.original_name" 
					:lang="serie.original_language"
					:vote="serie.vote_average"
					:poster="serie.poster_path"
					:plot="serie.overview"
					:image="`https://image.tmdb.org/t/p/w342${serie.poster_path}`">
					</Card>
				</div>
				<h4 v-else>Nessuna serie TV trovata</h4>
			</div>
		</div>
		<div v-else class="welcome mt-5">
			<h4>Benvenuto in Gringoflix, cerca un titolo per vedere i contenuti</h4>
		</div>
	</main>
</template>

<script>
import Card from './Card.vue'

export default {
	name: "Main",
	props: ["movieApi"],
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
h4 {
	color: white;
}
.welcome {
	text-align: center;
}
</style>
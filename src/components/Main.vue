<template>
	<main>
    	<ul v-if="inputHeader.movies.length > 0">
        	<li v-for="(movie, index) in inputHeader.movies" :key="index+'movies'">
				<div>Title: {{movie.title}}</div>
				<div>Original title: {{movie.original_title}}</div>
				<div>Language: <i :class="(movie.original_language == 'en') ? 'flag flag-us' : `flag flag-${movie.original_language}`"></i></div>
				<div>Vote: {{movie.vote_average}}</div>
			</li>
		</ul>
		<h2 v-else>Nessun film trovato</h2>
		<ul v-if="inputHeader.tv.length > 0">
			<li v-for="(movie, index) in inputHeader.tv" :key="index+'tv'">
				<div>Title: {{movie.name}}</div>
				<div>Original title: {{movie.original_name}}</div>
				<div>Language: <i :class="(movie.original_language == 'en') ? 'flag flag-us' : `flag flag-${movie.original_language}`"></i></div>
				<div>Vote: {{movie.vote_average}}</div>
			</li>
		</ul>
		<h2 v-else>Nessuna serie TV trovata</h2>
	</main>
</template>

<script>

export default {
	name: "Main",
	props: ["inputHeader"],
	data(){
		return {

		}
	}
}
</script>

<style lang="scss">

</style>
<template>
	<main>
    	<ul>
        	<li v-for="(movie, index) in inputHeader" :key="index">
				<div>{{movie.title}}</div>
				<div>{{movie.original_title}}</div>
				<div>{{movie.original_language}}</div>
				<div>{{movie.vote_average}}</div>
			</li>
    	</ul>
	</main>
</template>

<script>

export default {
	name: "Main",
	props: ["inputHeader"],
	data(){
	}
}
</script>

<style lang="scss">

</style>
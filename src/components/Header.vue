<template>
  <header>
		<div class="search">
			<input id="search" v-model="inputText" type="text" name="search">
			<button class="btn btn-primary" type="submit" @click="$emit('doSearch', inputText)"> Cerca</button>
		</div>
  </header>
</template>

<script>
export default {
	name: "Header",
	props: {
		inputValue: {
			type: String,
		}
	},
	data(){
		return {
			inputText: ''
		}
	}
}
</script>

<style lang="scss">

</style>
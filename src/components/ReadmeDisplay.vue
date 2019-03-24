<template>
	<div class="readme-display">
		<h5>Project Readme</h5>
		<div>Readme text will go here</div>
	</div>
</template>

<script>
export default {
	name: 'ReadmeDisplay',
	props: {
		readme: String
	}
}
</script>

<style scoped>
.readme-display {
	border: 1px solid black;
}
</style>

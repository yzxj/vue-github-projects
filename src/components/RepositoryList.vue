<template>
	<div class="repository-list">
		<p v-if="!username">Type in a username above and hit 'Enter' to get started!</p>
		<p v-else-if="!userIsValid">{{ username }} is not a valid user!</p>
		<div v-else-if="projects.length > 0">
			<h5>{{ username }}'s Projects</h5>
			<div v-for="repo in projects" v-bind:key="repo">
				<button v-on:click="$emit('select-project', repo)">
					{{ repo }}
				</button>
			</div>
		</div>
		<p v-else>{{ username }} has no public repos!</p>
	</div>
</template>

<script>
export default {
	name: 'RepositoryList',
	props: {
		username: String,
		userIsValid: Boolean,
		projects: Array,
	}
}
</script>

<style scoped>
</style>

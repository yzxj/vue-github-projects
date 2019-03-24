<template>
	<div class="repository-list">
		<p v-if="!searched">Type in a username above and hit 'Enter' to get started!</p>
		<p v-else-if="!validUser">{{ username }} is not a valid user!</p>
		<div v-else-if="repositories.length > 0">
			<h5>{{ username }}'s Projects</h5>
			<div v-for="repo in repositories">
				<button v-on:click="$emit('select-project', repo)">{{ repo }}</button>
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
		searched: Boolean,
		validUser: Boolean,
		repositories: Array,
	}
}
</script>

<style scoped>
.repository-list {
	border: 1px solid black;
}
</style>

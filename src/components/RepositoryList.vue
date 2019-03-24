<template>
	<div class="repository-list">
		<h5>UserX's Projects</h5>
		<ul>
			<li><a>Project 1</a></li>
			<li><a>Project 2</a></li>
			<li><a>Project 3</a></li>
		</ul>
	</div>
</template>

<script>
export default {
	name: 'RepositoryList',
	props: {
		// TODO: How to handle onClick?
		list: String
	}
}
</script>

<style scoped>
.repository-list {
	border: 1px solid black;
}
</style>

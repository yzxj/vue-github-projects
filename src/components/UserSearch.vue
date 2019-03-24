<template>
	<div class="user-search">
		<label>Username</label>
		<input placeholder="Whose projects would you like to look up?"/>
	</div>
</template>

<script>
export default {
	name: 'UserSearch',
	props: {
		input: String
	}
}
</script>

<style scoped>
.user-search {
	border: 1px solid black;
}
</style>

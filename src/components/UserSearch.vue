<template>
	<div class="user-search">
		<form v-on:submit.prevent="$emit('submit-username', username)">
			<label for="username">Github username</label>
			<br />
			<input
				class="username-input"
				name="username"
				placeholder="Whose projects would you like to look up?"
				v-model="username"
			/>
			<input type="submit" value="Search" />
		</form>
	</div>
</template>

<script>
export default {
	name: 'UserSearch',
	data: function () {
		return {
			username: ''
		}
	},
}
</script>

<style scoped>
.user-search {
	border: 1px solid black;
}
.username-input {
	width: 18vw;
}
</style>

<template>
	<div class="user-search">
		<form v-on:submit.prevent="$emit('submit-username')">
			<label for="username">Github username</label>
			<br />
			<input
				class="username-input"
				name="username"
				placeholder="Whose projects would you like to look up?"
				v-bind:value="value"
				v-on:input="$emit('input', $event.target.value)"
			/>
			<input type="submit" value="Search" />
		</form>
	</div>
</template>

<script>
export default {
	name: 'UserSearch',
	props: {
		value: String
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

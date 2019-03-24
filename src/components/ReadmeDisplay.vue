<template>
	<div class="readme-display">
		<h3 v-if="!project">README Viewer</h3>
		<h3 v-else>README of {{ project }}</h3>
		<div v-if="!project">
			<p>
				Get started by searching for a user on the left, and then selecting one of their projects.
			</p>
		</div>
		<div v-else-if="!readmeExists">
			<p class="error">
				Something went wrong when retrieving the README! This repo probably doesn't have a README file. Why don't you try another one?
			</p>
		</div>
		<div v-else-if="typeof readme !== 'string' || !readme.trim()">
			<p class="error">
				This repo doesn't seem to have a readme (or it's empty). Try another one!
			</p>
		</div>
		<div v-else>
			<hr />
			<div v-html="compiledMarkdown" />
		</div>
	</div>
</template>

<script>
import marked from 'marked';

export default {
	name: 'ReadmeDisplay',
	props: {
		readme: String,
		readmeExists: Boolean,
		project: String,
	},
	computed: {
		compiledMarkdown() {
			return marked(this.readme, { sanitize: true });
		}
	}
}
</script>

<style scoped>
.readme-display {
	overflow: scroll;
	text-align: left;
}
.error {
	color: red;
}
</style>

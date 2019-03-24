<template>
  <div id="app">
    <h1>Welcome to vue-github-projects</h1>
    <div class="grid-container">
      <UserSearch
        class="grid__top-left"
        v-model="username"
        v-on:submit-username="submitUsername"
      />
      <RepositoryList
        class="grid__bottom-left"
        v-bind:username="username"
        v-bind:repositories="repositories"
      />
      <ReadmeDisplay class="grid__right"
        v-bind:project="selectedProject"
        v-bind:readme="readme"
      />
    </div>
  </div>
</template>

<script>
import UserSearch from './components/UserSearch.vue'
import RepositoryList from './components/RepositoryList.vue'
import ReadmeDisplay from './components/ReadmeDisplay.vue'

const GITHUB_API = 'https://api.github.com/';

export default {
  name: 'app',
  components: {
    UserSearch,
    RepositoryList,
    ReadmeDisplay
  },
  data: function () {
    return {
      username: '',
      repositories: [],
      selectedProject: '',
      readme: ''
    };
  },
  methods: {
    async submitUsername() {
      const response = await fetch(`${GITHUB_API}users/${this.username}/repos`);
      const responseJson = await response.json();
      const repositoryNames = responseJson.map(repoObj => repoObj.name);
      this.repositories = repositoryNames;
    },
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  align-items: stretch;
  height: 100vh;
}
.grid-container {
  display: grid;
  grid-template-columns: 25% 75%;
  grid-template-rows: 25% 75%;
  grid-template-areas:
    "top-left right"
    "bottom-left right"
  ;
  flex: 1;
}
.grid__top-left {
  grid-area: top-left;
  display: flex;
  justify-content: center;
  align-items: center;
}
.grid__bottom-left {
  grid-area: bottom-left;
}
.grid__right {
  grid-area: right;
}
</style>

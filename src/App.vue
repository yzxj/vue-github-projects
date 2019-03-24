<template>
  <div id="app">
    <h1>Welcome to vue-github-projects</h1>
    <div class="grid-container">
      <UserSearch
        class="grid-el grid-el__top-left"
        v-model="username"
        v-on:submit-username="submitUsername"
      />
      <RepositoryList
        class="grid-el grid-el__bottom-left"
        v-bind:username="username"
        v-bind:userIsValid="userIsValid"
        v-bind:projects="projects"
        v-on:select-project="selectProject"
      />
      <ReadmeDisplay class="grid-el grid-el__right"
        v-bind:project="selectedProject"
        v-bind:readme="readme"
        v-bind:readmeExists="readmeExists"
      />
    </div>
  </div>
</template>

<script>
import UserSearch from './components/UserSearch.vue'
import RepositoryList from './components/RepositoryList.vue'
import ReadmeDisplay from './components/ReadmeDisplay.vue'

const GITHUB_API = 'https://api.github.com';
const README_HEADERS = {
  headers: {
    "Accept": "application/vnd.github.v3.raw+json"
  }
};

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
      userIsValid: false,
      projects: [],
      selectedProject: '',
      readme: '',
      readmeExists: false,
    };
  },
  methods: {
    async submitUsername(username) {
      try {
        const response = await fetch(`${GITHUB_API}/users/${username}/repos`);
        if (response.status !== 200) {
          throw new Error("Invalid user!");
        }
        const responseJson = await response.json();
        const repositoryNames = responseJson.map(repoObj => repoObj.name);

        this.projects = repositoryNames;
        this.userIsValid = true;
      } catch (err) {
        this.projects = [];
        this.userIsValid = false;
      }
      this.username = username;
      this.selectedProject = '';
      this.readme = '';
    },
    async selectProject(projectName) {
      try {
        const response = await fetch(
          `${GITHUB_API}/repos/${this.username}/${projectName}/readme`,
          README_HEADERS
        );
        if (response.status !== 200) {
          throw new Error("An error occurred while fetching the README!");
        }
        this.readme = await response.text();
        this.readmeExists = true;
      } catch (err) {
        this.readmeExists = false;
      }
      this.selectedProject = projectName;
    }
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
  height: 98vh;
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
  max-height: calc(98vh - 80px);
}
.grid-el {
  margin: 1px;
  padding: 12px;
  border: 1px solid black;
}
.grid-el__top-left {
  grid-area: top-left;
  display: flex;
  justify-content: center;
  align-items: center;
}
.grid-el__bottom-left {
  grid-area: bottom-left;
}
.grid-el__right {
  grid-area: right;
}
</style>

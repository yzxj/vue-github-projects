<template>
  <div id="app">
    <h1>Welcome to vue-github-projects</h1>
    <div class="grid-container">
      <UserSearch class="grid__top-left" />
      <RepositoryList class="grid__bottom-left" />
      <ReadmeDisplay class="grid__right" />
    </div>
  </div>
</template>

<script>
import UserSearch from './components/UserSearch.vue'
import RepositoryList from './components/RepositoryList.vue'
import ReadmeDisplay from './components/ReadmeDisplay.vue'

export default {
  name: 'app',
  components: {
    UserSearch,
    RepositoryList,
    ReadmeDisplay
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
}
.grid__bottom-left {
  grid-area: bottom-left;
}
.grid__right {
  grid-area: right;
}
</style>

<template>
  <div id="app">
    <h1 class="title is-1">Username's Github Project Portfolio</h1>
    <!-- <img src="./assets/logo.png"> -->
    <!-- <hello></hello> -->
    <project-list></project-list>
  </div>
</template>

<script>
import ProjectList from './components/Project-list'

export default {
  name: 'app',
  components: {
    ProjectList
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
  margin-top: 60px;
}

</style>

<template>
  <div id="app">
    <MoviePage/>
  </div>
</template>

<script>
import MoviePage from './components/MoviePage.vue'

export default {
  name: 'App',
  components: {
    MoviePage
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color:white;
}
body{
  background-color:rgb(90, 109, 213);

}
</style>

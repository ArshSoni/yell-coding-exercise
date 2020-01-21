<template>
  <div id="app">
    <input type="text" placeholder="Search for a movie" class="input-search" name="movie-search" v-model="movieSearch" />
    <Movies :search="movieSearch" />
  </div>
</template>

<script>
import Movies from './components/Movies.vue';

export default {
  name: "App",
  components: {
    Movies
  },

  data: () => {
    return {
      movieSearch: null
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  background: #1b1b1b;
  color: #ccc;
}

#app {
  padding: 2em;
  font-family: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, Oxygen,
    Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
}

.input-search {
  display: block;
  width: 100%;
  margin-bottom: 1em;
  background: transparent;
  -webkit-appearance: none;
  border: 0;
  font-size: 1.4em;
  outline: 0;
  color: white;
  font-family:-apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen,Ubuntu,Cantarell,Fira Sans,Droid Sans,Helvetica Neue,sans-serif;
}


</style>

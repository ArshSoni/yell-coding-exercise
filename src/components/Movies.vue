<template>
  <div>
    <p>Searching for <b>{{ defaultSearch }}</b></p>
    <ul class="movies">
      <li v-for="movie in getMovies" :key="movie.title" class="movies--item">
        <img class="movies--image" :src="posterPath + movie.poster_path">
        <div class="movies--meta">
          <h2 class="movies--title">{{ movie.title }}</h2>
          <p class="movies--star">
            <span>⭐️</span>
            {{ Math.round(movie.vote_average) }}
          </p>
          <p class="movies--desc">{{ movie.overview }}</p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Movies",

  props: {
    search: {
      type: String,
      default: ""
    },
    
    defaultSearch: {
      type: String,
      default: 'marvel'
    }
  },

  data() {
    return {
      data: [],
      movies: [],
      apiKey: "1b62ccff88d2cd537027e1d82920197b",
      url: "https://api.themoviedb.org/3/search/movie",
      posterPath: "https://image.tmdb.org/t/p/w342"
    };
  },

  mounted() {
    this.fetchMovies();
  },

  computed: {
    getUrl() {
      const { url, apiKey, defaultSearch } = this;
      return `${url}?api_key=${apiKey}&query='${defaultSearch}'`;
    },

    getMovies() {
      const { search, movies } = this;
      if (search) {
        return movies.filter(i => i.title.toLowerCase().includes(search.toLowerCase()));
      }
      return movies;
    }
  },

  methods: {
    fetchMovies() {
      axios.get(this.getUrl).then(res => {
        this.data = res.data;
        this.movies = res.data.results;
      });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.movies {
  list-style: none;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  grid-gap: 1em;
}

.movies--image {
  max-width: 100%;
  height: auto;
  display: block;
  border-radius: 8px;
}

.movies--item {
  position: relative;
  overflow: hidden;
}

.movies--item:hover .movies--desc {
  max-height: 200px;
}

.movies--item::after {
  position: absolute;
  top: 0;
  left: 0;
  width: calc(100% + 1px);
  height: calc(100% + 1px);
  content: "";
  background-image: linear-gradient(transparent, rgba(0, 0, 0, 0.8) 80%);
  border-radius: 8px;
}

.movies--meta {
  position: absolute;
  z-index: 1;
  bottom: -10px;
  padding: 1em;
  padding-bottom: 20px;
}

.movies--title {
  font-size: 0.9em;
  font-weight: 600;
  margin-bottom: 5px;
}

p {
  font-size: 0.9em;
}

p > * {
  display: inline-block;
  vertical-align: middle;
}
p > span {
  margin-right: 2px;
}

input {
  display: block;
  width: 100%;
  margin-bottom: 1em;
  background: transparent;
  -webkit-appearance: none;
  border: 0;
  font-size: 1.4em;
  outline: 0;
  color: white;
  font-family: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, Oxygen,
    Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
}

.movies--star {
  padding-bottom: 10px;
}

.movies--desc {
  position: relative;
  height: 3.9em;
  overflow: hidden;
  line-height: 1.3;
  font-size: 12px;
  max-height: 0;
  transition: max-height 300ms linear;
}
</style>

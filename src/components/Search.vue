<template>
  <div class="search">
    <h1>Search</h1>
    <input type="text" v-model='query' @keyup="getResult(query)">
    <div v-for='result in results' :key='result.id'>
      <p>{{result.title}}</p>
      <img v-bind:src="'http://image.tmdb.org/t/p/w500/' + result.poster_path" alt=result.title width='100px'>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

// const REQUEST = 'https://api.themoviedb.org/3/search/movie?api_key=f86cc31e3850cd90ef8e189703f28ac1query=';

function createRequest(query) {
  const API_KEY = 'f86cc31e3850cd90ef8e189703f28ac1';
  const REQUEST = `https://api.themoviedb.org/3/search/movie?api_key=${API_KEY}&language=en-US&query=${query}&page=1&include_adult=false`;
  return REQUEST;
}

export default {
  name: 'search',
  data() {
    return {
      query: '',
      results: '',
    };
  },
  methods: {
    getResult(query) {
      axios.get(createRequest(query)).then((response) => { this.results = response.data.results; });
      console.log(this.results);
    },
  },
};
</script>

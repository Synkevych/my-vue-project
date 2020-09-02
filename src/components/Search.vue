<template>
  <div class="search">
      <b-form @submit="onSubmit" @reset="onReset" v-if="show">
        <b-form-group
          id="input-group-1"
          label="Search "
          label-for="input-1"
          description="We'll never share your email with anyone else.">
          <h1>Search</h1>
          <b-form-input
            id="input-1"
            type="text"
            required
            placeholder="Enter email"
            v-model='query' @keyup="getResult(query)"
          ></b-form-input>
        </b-form-group>
      </b-form>
    <!-- <input type="text" v-model='query' @keyup="getResult(query)"> -->
      <b-container fluid class="p-4 bg-dark">
        <b-row>
          <div v-for='result in results' :key='result.id'>
            <b-col class="mr-3">
              <b-img v-bind:src="'http://image.tmdb.org/t/p/w500/' + result.poster_path" width='200px' alt="Image"></b-img>
              <p>{{result.title}}</p>
            </b-col>
          </div>
        </b-row>
      </b-container>
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

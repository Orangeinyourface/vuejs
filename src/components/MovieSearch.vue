<template>
  <div>
    <v-text-field v-model="searchText" label="Rechercher un film" @keyup.enter="searchMovies"></v-text-field>
  </div>
</template>
  
  <script>
  import axios from 'axios'
  import config from '@/config.json'
  
  export default {
    name: 'MovieSearch',
    data() {
      return {
        searchText: '',
      }
    },
    methods: {
      searchMovies() {
        axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${config.api_key}&query=${this.searchText}`)
          .then(response => {
            this.$emit('update-movies', response.data.results);
          })
          .catch(error => {
            console.error(error);
          })
      }
    }
  }
  </script>
  
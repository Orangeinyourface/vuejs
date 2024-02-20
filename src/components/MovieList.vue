<template>
  <div>
    <v-row>
      <v-col v-for="movie in movies" :key="movie.id" cols="12" sm="6" md="4">
        <v-card>
          <v-img v-if="movie.poster_path" :src="getImgUrl(movie.poster_path)"></v-img>
          <v-img v-else src=""></v-img>
          <v-card-title>{{ movie.title }}</v-card-title>
          <v-btn @click="goToMovieDetail(movie.id)">Plus d'information</v-btn>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<style scoped>
.v-img {
  height: 200px;
  object-fit: cover;
}
</style>

<script>
import axios from 'axios'
import config from '@/config.json'

export default {
  name: 'MovieList',
  props: {
    page: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      movies: [],
    }
  },
  watch: {
    page() {
      this.fetchMovies();
    }
  },
  created() {
    this.fetchMovies();
  },
  methods: {
    fetchMovies() {
      axios.get(`${config.url.movie_list}?api_key=${config.api_key}&page=${this.page}`, {
        headers: {
          'Authorization': `Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiJlNTJhYWMxZjZkNjc5Y2VmZTY1NTVmNTU1MmQ2NjQ5MiIsInN1YiI6IjY1YzEwMTRjNWUxMjAwMDE4MjFjZTY3MSIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.dk-d3bM2Q4t3waNQkkxKQaDfnTxm0YFo2YC_r1SvPDM`
        }
      })
      .then(response => {
        this.movies = response.data.results;
        console.log(this.movies);
      })
      .catch(error => {
        console.error(error);
      })
    },
    getImgUrl(path) {
      return `${config.url.photo_path}${path}`;
    },
    goToMovieDetail(movieId) {
      this.$router.push({ name: 'movieDetail', params: { id: movieId } });
    }
  }
}
</script>

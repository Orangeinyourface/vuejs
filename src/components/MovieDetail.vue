<template>
  <div>
    <h1>{{ movie.title }}</h1>
    <v-img :src="getImgUrl(movie.poster_path)" max-height="500px"></v-img>
    <div v-if="$route.path.startsWith('/movie/')">
      <h1>Genres : </h1>
      <p>{{ genres }}</p>
    </div>
    <h1>Synopsis : </h1>
    <p>{{ movie.overview }}</p>

    <v-btn @click="goBack">Retour</v-btn>
  </div>
</template>

<script>
import axios from 'axios'
import config from '@/config.json'

export default {
  name: 'MovieDetail',
  data() {
    return {
      movie: {},
    }
  },
  computed: {
    genres() {
      if (this.movie && this.movie.genres) {
        return this.movie.genres.map(genre => genre.name).join(', ');
      } else {
        return '';
      }
    }
  },
  created() {
    this.fetchMovieDetail()
  },
  methods: {
    fetchMovieDetail() {
      const movieId = this.$route.params.id
      axios.get(`https://api.themoviedb.org/3/movie/${movieId}?api_key=${config.api_key}&language=fr`)
        .then(response => {
          this.movie = response.data;
        })
        .catch(error => {
          console.error(error);
        })
    },
    getImgUrl(path) {
      return `${config.url.photo_path}${path}`;
    },
    goBack() {
    this.$router.go(-1);
  }
  }
}
</script>

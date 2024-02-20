<template>
  <div>
    <MovieSearch @update-movies="updateMovies"></MovieSearch>
    <MovieList :movies="movies" :page="currentPage" @change-page="handleChangePage"></MovieList>
    <MovieDetail></MovieDetail>
    <MoviePagination :currentPage="currentPage" @change-page="handleChangePage"></MoviePagination>
  </div>
</template>

<script>
import MovieSearch from '@/components/MovieSearch.vue'
import MovieList from '@/components/MovieList.vue'
import MovieDetail from '@/components/MovieDetail.vue'
import MoviePagination from '@/components/MoviePagination.vue'

export default {
  name: 'HomeView',
  data() {
    return {
      currentPage: 1,
      movies: [],
    }
  },
  components: {
    MovieSearch,
    MovieList,
    MovieDetail,
    MoviePagination
  },
  methods: {
    handleChangePage(page) {
      this.currentPage = page;
    },
    updateMovies(movies) {
      this.movies = movies;
    }
  }
}
</script>

<template>
  <div class="home">
    <!-- Hero -->
    <Hero />
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      movies: [],
    }
  },
  async fetch() {
    await this.getMovies()
  },
  methods: {
    async getMovies() {
      const response = await axios.get(
        'https://api.themoviedb.org/3/movie/now_playing',
        {
          params: {
            api_key: process.env.TMDB_API,
            page: 1,
          },
        }
      )

      const data = response.data

      data.results.forEach((movie) => {
        this.movies.push(movie)
      })
    },
  },
}
</script>

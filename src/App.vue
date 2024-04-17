<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
import SearchFilm from './components/SearchFilm.vue';
import FilmList from './components/FilmList.vue';

export default {
  components: {
    AppHeader,
    SearchFilm,
    FilmList
  },
  data() {
    return {
      searchResults: []
    };
  },
  methods: {
    async searchFilms(query) {
      try {
        const response = await axios.get(
          `https://api.themoviedb.org/3/search/movie`,
          {
            params: {
              api_key: 'YOUR_API_KEY',
              query: query
            }
          }
        );
        this.searchResults = response.data.results;
      } catch (error) {
        console.error('Error fetching movies:', error);
      }
    }
  }
};
</script>

<template>
  <div>
    <AppHeader />
    <SearchFilm @search="searchFilms" />
    <div v-if="searchResults.length">
      <FilmList :films="searchResults" />
    </div>
  </div>
</template>

<style lang="scss" scoped>

</style>

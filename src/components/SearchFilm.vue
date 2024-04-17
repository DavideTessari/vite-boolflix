<template>
    <div>
      <input v-model="searchQuery" placeholder="Search movies and TV shows..." />
      <button @click="search">Search</button>
      <div v-if="searchResults.length">
        <div v-for="result in searchResults" :key="result.id" class="search-result">
          <img
            v-if="result.poster_path"
            :src="'https://image.tmdb.org/t/p/w342/' + result.poster_path"
            alt="Poster"
          />
          <div class="result-info">
            <h3>{{ result.title || result.name }}</h3>
            <p>{{ result.original_title || result.original_name }}</p>
            <div v-if="result.original_language">
              <img
                :src="getFlag(result.original_language)"
                :alt="result.original_language + ' flag'"
                class="language-flag"
              />
            </div>
            <p>Rating: {{ Math.ceil(result.vote_average / 2) }}/5</p>
            <p>{{ result.overview }}</p>
          </div>
        </div>
      </div>
    </div>
</template>
  
<script>
  import axios from 'axios';
//   import { countryFlag } from 'country-flag-icons'; 
  
  export default {
    data() {
      return {
        searchQuery: '',
        searchResults: []
      };
    },
    methods: {
      async search() {
        try {
          const movieResponse = await axios.get('https://api.themoviedb.org/3/search/movie', {
            params: {
              api_key: 'dd6f748407d41158f1d47125a3b3fd33',
              query: this.searchQuery
            }
          });
  
          const tvResponse = await axios.get('https://api.themoviedb.org/3/search/tv', {
            params: {
              api_key: 'dd6f748407d41158f1d47125a3b3fd33',
              query: this.searchQuery
            }
          });
  
          this.searchResults = [...movieResponse.data.results, ...tvResponse.data.results];
        } catch (error) {
          console.error('Error fetching search results:', error);
        }
      },
      getFlag(language) {
        // Restituisce l'URL della bandiera corrispondente alla lingua
        const flag = countryFlag(language);
        return flag ? flag.svg : '';
      }
    }
  };
</script>
  
<style scoped>
  .language-flag {
    width: 24px;
    height: 24px;
    margin-right: 5px;
  }
  .search-result {
    display: flex;
    align-items: center;
    margin-bottom: 20px;
  }
  .result-info {
    margin-left: 10px;
  }
  .result-info h3 {
    margin-bottom: 5px;
  }
</style>
  
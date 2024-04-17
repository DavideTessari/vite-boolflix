<template>
    <div>
      <div v-for="film in films" :key="film.id" class="film-item">
        <img :src="'https://image.tmdb.org/t/p/w342/' + film.poster_path" alt="Poster" />
        <h3>{{ film.title }}</h3>
        <p>{{ film.original_title }}</p>
        <p>{{ film.original_language }}</p>
        <p>Rating: {{ Math.ceil(film.vote_average / 2) }}/5</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['films']
  };
  </script>
  
  <style scoped>
  .film-item {
    border: 1px solid #ccc;
    padding: 10px;
    margin-bottom: 10px;
  }
  .film-item img {
    max-width: 100%;
  }
  </style>
  
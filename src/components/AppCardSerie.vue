<script>
import { store } from '../store';

export default {
  name: 'AppCardSerie',
  data() {
    return {
      store,
      languageImage: [
        "it.jpg",
        "en.jpg",
        "ja.jpg", 
        "fr.jpg",
        "de.jpg",
        "es.jpg",
        "ko.jpg",
        "ru.jpg"
      ]
    };
  },
  methods: {
    getImageLanguage(img) {
      return new URL(`../assets/${img}`, import.meta.url).href;
    },
    posterImg(link) {
      const posterLink = 'https://image.tmdb.org/t/p/w500/';
      if (link === null || link === undefined || link === '') {
        return 'https://www.tgv.com.my/assets/images/404/movie-poster.jpg';
      } else {
        return posterLink + link;
      }
    }
  }
};
</script>

<template>
  <div>
    <section>
      <h2>Serie</h2>
      <div class="flex wrap">
        <div v-for="serie in store.series" :key="serie.id" class="card relative hover">
          <img :src="posterImg(serie.poster_path)" alt="Series Poster" class="poster">
          <div class="cardInfo">
            <h3>Original Title: <br>{{ serie.original_name }}</h3>
            <h3>Film Title: <br>{{ serie.name }}</h3>
            <div v-if="languageImage.includes(serie.original_language + '.jpg')">
              <span>Original Language: </span>
              <img :src="getImageLanguage(serie.original_language + '.jpg')" alt="Country Flag" class="flag">
            </div>
            <div v-else>
              {{ serie.original_language }}
            </div>
            <span class="star"><i class="fa-solid fa-star" v-for="star in Math.ceil(serie.vote_average / 2)" :key="star" /></span>
            <span class="empty-star"><i class="fa-solid fa-star" v-for="emptyStar in 5 - Math.ceil(serie.vote_average / 2)" :key="emptyStar" /></span>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<style lang="scss" scoped>
@import '../style/general.scss';

section {
  width: 85%;
  min-height: 500px;
  color: white;
  margin: 0 auto;
  padding-top: 2rem;
  padding-bottom: 2rem;
}

.poster {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: all 1s ease-in;
}

.card {
  width: calc(100% / 5 - 2rem);
  margin: 0.4rem;
  background-color: #2b2a33;
  color: white;
  position: relative;

  .cardInfo {
    display: block;
    opacity: 0;
  }

  .flag {
    width: 25px;
    height: 15px;
  }
}

.card:hover {
  .cardInfo {
    opacity: 1;
  }
  .poster {
    height: 45%;
  }
}
</style>

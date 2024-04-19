<script>
import { store } from '../store';

export default {
    name: 'AppCardFilm',
    data() {
        return {
            store,
            languageImage: [
                "it.jpg", "en.jpg", "ja.jpg", "fr.jpg", "de.jpg", "es.jpg", "ko.jpg", "ru.jpg"
            ],
        };
    },
    methods: {
        getImageLanguage(img) {
            return new URL(`../assets/${img}`, import.meta.url).href;
        },
        posterImg(link) {
            if (link === null || link === undefined) {
                return 'https://www.tgv.com.my/assets/images/404/movie-poster.jpg';
            }
            return `https://image.tmdb.org/t/p/w500/${link}`;
        },
     },
};
</script>


<template>
    <section>
        <h2>FILM</h2>
        <div class="flex wrap">
            <div v-for="movie in store.movies" :key="movie.id" class="card">
                <img :src="posterImg(movie.poster_path)" alt="Movie Poster" class="poster">
                <div class="card-info">
                    <h3>Original Title: {{ movie.original_title }}</h3>
                    <h3>Film Title: {{ movie.title }}</h3>
                    <div v-if="languageImage.includes(movie.original_language + '.jpg')">
                        <span>Original Language:</span>
                        <img :src="getImageLanguage(movie.original_language + '.jpg')" alt="Country Flag" class="flag">
                    </div>
                    <div v-else>
                        {{ movie.original_language }}
                    </div>
                    <span class="star">
                        <i class="fa-solid fa-star" v-for="star in Math.ceil(movie.vote_average / 2)" :key="star"/>
                    </span>
                    <span class="empty-star">
                        <i class="fa-solid fa-star" v-for="emptyStar in 5 - Math.ceil(movie.vote_average / 2)" :key="emptyStar"/>
                    </span>
                </div>
            </div>
        </div>
    </section>
</template>


<style lang="scss" scoped>
@use '../style/general.scss';

section {
    width: 95%;
    min-height: 500px;
    margin: 0 auto;
    color: white;

    h2{
      font-size: 40px;
      text-align: center;
      color: red;
      font-weight: bold;
      padding: 30px;
    }

    .poster {
        width: 100%;
        height: 100%;
        object-fit: cover;
        transition: all 0.5s ease-in-out;
    }

    .card {
        width: calc(20% - 0.8rem);
        margin: 0.4rem;
        background-color: #2b2a33;
        color: white;
        position: relative;

        &:hover {
            .card-info {
                opacity: 1;
            }
            .poster {
                height: 0%;
            }
        }

        .card-info {
            display: block;
            opacity: 0;
        }

        .flag {
            width: 25px;
            height: 15px;
        }
    }

    .star{
      i {
            font-size: 1rem;
            color: gold;
        }
    }
    .empty-star {
        i {
            font-size: 1rem;
            color: white;
        }
    }
}
</style>

<script>
import { store } from '../store';
import AppCardFilm from './AppCardFilm.vue';
import AppCardSerie from './AppCardSerie.vue';
export default {
    name: 'AppMain',
    components: {
    AppCardFilm ,
    AppCardSerie
    },
    data(){
        return{
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
            ],
            cardVisible: false
        }
    },
    methods:{
        getImageLanguage: function (img) {
            return new URL(`../assets/${img}`, import.meta.url).href;
        },     
        posterImg(link){
            let posterLink = 'https://image.tmdb.org/t/p/w500/'
            if(link === null){
                posterLink = 'https://www.tgv.com.my/assets/images/404/movie-poster.jpg'
            }else{
                posterLink += link
            }
            return posterLink
        },
        visibleInfo(){
            this.cardVisible = !this.cardVisible
        }
    },
}
</script>

<template>
    <main>
        <AppCardFilm/>
        <AppCardSerie/>
    </main>
</template>

<style lang="scss" scoped>
@use '../style/general.scss' as *;
    main{
        background-color: #2b2a33;
        min-height: 85vh;
    }
</style>
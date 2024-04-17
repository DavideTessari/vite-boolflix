
<script>
import {store} from '../store';
import FilmList from './FilmList.vue';
import SeriesList from './SeriesList.vue';


export default {
    data(){
        return{
            store,
        }
    },

    components:{
        FilmList,
        SeriesList,
    }

}
</script>


<template>
    <main>
        <FilmList/>
        <SeriesList/>
    </main>
    
</template>

<style scoped>


</style>
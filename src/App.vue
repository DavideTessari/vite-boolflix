<script >
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
import axios from 'axios';
import { store } from './store';
import AppCardFilm from './components/AppCardFilm.vue';
import AppSearchbar from './components/AppSearchbar.vue';

export default{
  name: 'App',
  components:{
    AppHeader,
    AppMain,
    AppCardFilm,
    AppCardSerie,
    AppSearchbar,
  },
  data(){
    return{
      store,
    }
  }
}
</script>

<template>
  <div>
    <AppHeader/>
    <AppMain/>
  </div>
</template>

<style lang="scss">
@import './style/general.scss';
@import './style/partials/_variables.scss';
</style>
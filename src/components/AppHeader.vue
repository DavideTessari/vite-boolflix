<script>
import AppSearchbar from './AppSearchbar.vue';
export default {
  name: 'AppHeader',
  data(){
      return{
          
      }
  },
  components:{
    AppSearchbar,
  }
}
</script>

<template>
  <div class="flex">
      <h1 class="logo">BOOLFLIX</h1>
      <AppSearchbar/>
  </div>
</template>

<style lang="scss" scoped>
  @use '../style/general.scss';
  div{
    background-color: black;
  }
  .logo{
    padding: 25px;
    width: 150px;
  }
</style>
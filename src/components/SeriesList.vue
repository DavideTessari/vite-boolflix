<script>
import { store } from '../store';
import CountryFlag from "vue-country-flag-next";

// import LangFlag from 'vue-lang-code-flags';


export default {
data(){
    return{
        store,
    

    }
},

components:{
    CountryFlag,
    // LangFlag,
},


}
</script>



<template>
 
  

</template>



<style lang="scss"  scoped>
@use '../style/partials/variables.scss'as *;

</style>
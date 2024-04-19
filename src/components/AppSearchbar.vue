<script>
import { store } from '../store';
import axios from 'axios';
export default {
    name: 'AppSearchbar',

    data(){
        return{
            store,
            researchText:'',
            apiUrl:'https://api.themoviedb.org/3/search/',
            tokenAcces: 'api_key=dd6f748407d41158f1d47125a3b3fd33',
        }
    },
    methods: {
        searchMovie(search){
            axios.get(`${this.apiUrl}movie?${this.tokenAcces}&query=${search}`)
            .then((response)=>{
                this.store.movies=response.data.results;
                console.log(response.data.results)
            })
            axios.get(`${this.apiUrl}tv?${this.tokenAcces}&query=${search}`)
            .then((response)=>{
                this.store.series= response.data.results;
                console.log(response.data.results)
            })
        }
    },
}
</script>

<template>
    <div class="searchbar">
        <i class="fa-solid fa-magnifying-glass icon"></i>
        <input type="text" v-model="researchText" @keyup.enter="searchMovie(researchText)" placeholder="Search a film/serie tv">
        <button @click="searchMovie(researchText), researchText=''">Search film</button>
    </div>
</template>
  
<style lang="scss" scoped>
    .searchbar{
        margin:1.5rem 1.5rem;
    }
      
    .icon{
        color: white;
        margin-right: 1.5rem;
    }
    input{
        height: 35px;
        border-radius: 15px;
        padding: 0.5rem;
    }
    button{
        padding: 0.5rem;
        border-radius: 15px;
        margin-left: 1rem;
    }
</style>

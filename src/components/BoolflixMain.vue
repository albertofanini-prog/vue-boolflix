<template>
    <main>
        <input
        type="text"
        placeholder="Scrivi qua..."
        v-model="searchMovie"
        >
        <button @click="searchAPI(searchMovie)">
            Search
        </button>
        <div
        class="singleMovie"
        v-for="movie in movies"
        :key="movie.id"
        >
            <h3>{{movie.title}}</h3>
            <h4>{{movie.original_title}}</h4>
            <h6>{{movie.original_language}}</h6>
            <h6>{{movie.vote_average}}</h6>
        </div>
    </main>
</template>

<script>

import axios from 'axios'

export default {
    name: 'BoolflixMain',
    data(){
        return{
            searchMovie: '',
            movies:[]
        }
    },
    methods: {
        searchAPI(input){
            this.searchMovie = input;
            axios.get(
                `https://api.themoviedb.org/3/search/movie?api_key=21468023db35f90fc29dfeda12ec6478&language=en-US&query=`
                +   
                this.searchMovie
                +
                `&page=1&include_adult=false`
            )
            .then((response) =>{
                this.movies = response.data.results;
            })
            // ,{
            //     params:{
            //         apiKey: '21468023db35f90fc29dfeda12ec6478',
            //         query: this.searchMovie,
            //     }
            // }
        }
    },
    // created(){
    //     axios.get('https://api.themoviedb.org/3/movie/550?api_key=21468023db35f90fc29dfeda12ec6478')
    // }
}
</script>

<style lang="scss">

</style>
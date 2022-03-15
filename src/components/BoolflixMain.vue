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
        <div class="movies_container">
            <div
            class="singleMovie"
            v-for="movie in movies"
            :key="movie.id"
            >
                <h1>{{movie.title}}</h1>
                <h3>{{movie.original_title}}</h3>
                <h4>Lingua originale: {{movie.original_language}}</h4>
                <h4>Voto medio: {{movie.vote_average}}</h4>
            </div>
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
            movies:[],
            baseUrl: 'https://api.themoviedb.org/3'
        }
    },
    methods: {
        searchAPI(input){
            this.searchMovie = input;
            axios.get( `${this.baseUrl}/search/movie`,{
                params: {
                    language: 'it-IT',
                    api_key: '21468023db35f90fc29dfeda12ec6478',
                    query: this.searchMovie,
                }
            })
            .then((response) =>{
                this.movies = response.data.results;
            })
        }
    },
    // created(){
    //     axios.get('https://api.themoviedb.org/3/movie/550?api_key=21468023db35f90fc29dfeda12ec6478')
    // }
}
</script>

<style lang="scss">
    .movies_container{
        margin-top: 10px;
        padding: 10px 20px;
        width: 100%;
        // border: 1px solid blue;
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
        gap: 10px;
        .singleMovie{
            // border: 1px solid red;
            width: 23%;
            padding: 15px;
            background-color: #2c3e50;
            border-radius: 25px;
        } h1{
            color: red;
        } h1{
            color: silver;
        } h4{
            color: gold;
        }
    }
</style>
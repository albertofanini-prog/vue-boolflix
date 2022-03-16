<template>
    <main>
        <!-- <div class="form_container">
        <form action=""> -->
            <input
            class="input_1"
            type="text"
            placeholder="Scrivi qua..."
            v-model="searchMovie"
            >
            <button
            class="input_2"
            @click="searchAPI(searchMovie)">
            Search
            </button>
        <!-- </form>
        </div> -->

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
            baseUrl: 'https://api.themoviedb.org/3',
            flags:[
                {
                    country: "it",
                    icon: "./assets/Flags/it.svg"
                },
            ]
        }
    },
    methods: {
        searchAPI(input){
            this.searchMovie = input;
            axios.get( `${this.baseUrl}/search/movie`,{
                params: {
                    api_key: '21468023db35f90fc29dfeda12ec6478',
                    query: this.searchMovie,
                    language: this.flagShow,
                }
            })
            .then((response) =>{
                this.movies = response.data.results;
            })
        },
    },
}
</script>

<style lang="scss">
    // .form_container{
    //     display: flex;
    //     align-items: center;
    //     justify-content: center;
    //     overflow: hidden;
    //     padding-top: 15px;
    //     form{
    //         position: relative;
    //     }
    //     .input_1{
    //         display: block;
    //         width: 100%;
    //         padding: 10px 20px 10px 10px;
    //         border: 2px solid #e50913;
    //         border-radius: 20px;
    //         color: #e50913;
    //     }

    //     .input_1::placeholder{
    //         color: #e50913;
    //     }

    //     .input_2{
    //         position: absolute  ;
    //         right: 5px;
    //         top: 5px;
    //         display: block;
    //         width: 40%;
    //         padding: 5px 20px 5px 10px;
    //         background-color: #e50913;
    //         border: 2px solid #e50913;
    //         border-radius: 0 20px 20px 0;
    //         color: #fff;
    //         transition: 0.5 ease;
    //     }

    //     .input_2:active{
    //         transform: scale(0.9);
    //     }
    // }
    input{
        height: 25px;
        width: 15%;
        margin-top: 10px;
        margin-right: 10px;
        border-radius: 999px;
        padding: 10px;
        background-color: white;
    }
    button{
        height: 25px;
        margin-top: 10px;
        padding: 5px 10px;
        border-radius: 999px;
        cursor: pointer;
        background-color: gray;
    }
    input:focus{
    outline:none;
    }
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
            background-color: #1b1e23;
            border-radius: 25px;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 5px;
            border: 4px solid white;
        } h1{
            color: red;
            height: 50%;
            background-color: none;
        } h3{
            color: gold;
            height: 20%;
        } h4{
            color: silver;
            height: 20%;
        }
    }
</style>
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
            @click="searchMovieAPI(searchMovie); searchTvSerieAPI(searchTvSerie)">
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
                <img class="poster" :src="`https://image.tmdb.org/t/p/w342${movie.poster_path}`" alt="">
                <div class="movie_info">
                    <span id="title">
                        {{movie.title}}
                    </span>
                    <span id="original_title">
                        {{movie.original_title}}
                    </span>
                    <span id="original_language">
                        <span> Lingua originale: </span><img class="flag" :src="'Flags/' + movie.original_language + '.svg'">
                    </span>
                    <div id="average_vote">
                        Voto medio: 
                        <span 
                        :class="i < getMovieVoteAverage(movie) ? 'star' : ''"
                        v-for="(starIcon, i) in 5"
                        :key="i"
                        >
                            &#9733;
                        </span>
                    </div>
                </div>
                <!-- <h2>{{movie.title}}</h2>
                <h3>{{movie.original_title}}</h3>
                <h4>Lingua originale: <img :src="'Flags/' + movie.original_language + '.svg'"></h4>
                <div>Voto medio: 
                    <span 
                    :class="i < getMovieVoteAverage(movie) ? 'star' : ''"
                    v-for="(starIcon, i) in 5"
                    :key="i"
                    >
                    &#9733;
                    </span>
                </div> -->
                
            </div>
            <!-- <div
            class="singleMovie"
            v-for="serie in series"
            :key="serie.id"
            >
                <img :src="`https://image.tmdb.org/t/p/w342${serie.poster_path}`" alt="serie.name">
                <h2>{{serie.name}}</h2>
                <h3>{{serie.original_name}}</h3>
                <h4>Lingua originale: <img :src="'Flags/' + movie.original_language + '.svg'"></h4>
                <h4>Voto medio: {{serie.vote_average}}</h4>
            </div> -->
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
            searchTvSerie: '',
            movies:[],
            series:[],
            baseUrl: 'https://api.themoviedb.org/3',
        }
    },
    methods: {
        searchMovieAPI(input){
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
                console.log(response.data);
            })
        },
        searchTvSerieAPI(input){
            this.searchTvSerie = input;
            axios.get( `${this.baseUrl}/search/tv`,{
                params: {
                    api_key: '21468023db35f90fc29dfeda12ec6478',
                    query: this.searchMovie,
                    language: this.flagShow,
                }
            })
            .then((response) =>{
                this.series = response.data.results;
                console.log(response.data);
            })
        },
        getMovieVoteAverage: function (movie){
            return Math.ceil(movie.vote_average / 2);
        },
        getSerieVoteAverage: function (serie){
            return Math.ceil(serie.vote_average / 2)
        }
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
    main{
        //border: 3px dashed yellow;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }
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
        // padding: 10px 20px;
        width: 80%;
        // border: 1px solid blue;
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        align-items: center;
        gap: 30px;
        //border: 3px solid purple;
        .singleMovie{
            // border: 1px solid red;
            width: calc((100% / 6) - 30px);
            height: 350px;
            // padding: 15px;
            background-color: #1b1e23;
            // //border-radius: 25px;
            // display: flex;
            // flex-direction: column;
            // align-items: center;
            // gap: 5px;
            border: 4px solid white;
            position: relative;
            .poster {
            width: 100%;
            height: 100%;
            // opacity: 0.2;
        } .movie_info{
            color: white;
            position: absolute;
            top: 10%;
            left: 10%;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            display: none;
            #title{
            height: 30%;
            font-size: 22px;
            font-weight: 600;
            padding: 5px;
            } #original_title{
            height: 20%;
            font-size: 18px;
            padding: 5px;
            } #original_language{
            height: 30%;
            font-size: 14px;
            padding: 5px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
                span{
                    padding: 5px;
                }
                img{
                    max-width: 30%;
                    max-height: 20%;
                }
            } #average_vote{
                height: 20%;
            }
        } .poster:hover{
            opacity: 0.2;
        } .movie_info:hover{
            display: block;
        }
    }
}
    .star{
        color: gold;
    }
</style>
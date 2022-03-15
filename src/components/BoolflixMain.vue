<template>
    <main>
        <input type="text" placeholder="Scrivi qua">
        <button>Search</button>
    </main>
</template>

<script>

import axios from 'axios'

export default {
    name: 'BoolflixMain',
    data(){
        return{
            search: 'fight club',
            movies:[]
        }
    },
    created(){
        axios.get('https://api.themoviedb.org/3/movie/550?api_key=21468023db35f90fc29dfeda12ec6478')
    }
}
</script>

<style lang="scss">

</style>
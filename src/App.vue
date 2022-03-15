<template>
  <div id="app">
    <img alt="Netflix logo" src="./assets/logoNetflix.png">
    <BoolflixMain/>
  </div>
</template>

<script>
import BoolflixMain from './components/BoolflixMain.vue'

export default {
  name: 'App',
  components: {
    BoolflixMain
  }
}
</script>

<style lang="scss">
*{
  border: 0;
  margin: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  img{
    max-width: 100px;
    max-height: 100px;
  };
}
</style>

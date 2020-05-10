<template>
  <div id="app">
    <img class="test" alt="Vue logo" src="./assets/logo.png">
    <infinite-slider />
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import InfiniteSlider from './components/InfiniteSlider.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
    InfiniteSlider,
  },
}
</script>

<style lang="scss">
#app {
    position: relative;
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>

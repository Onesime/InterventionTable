<template>
  <div id="app">
    Hello
    <img src="./assets/logo.png">
    World
    <helloworld></helloworld>
    <router-view/>
  </div>
</template>

<script>

import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  components: {
      helloworld:HelloWorld
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

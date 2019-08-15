<template>
  <div id="app">
    <codemirror></codemirror>
<!--    <img alt="Vue logo" src="./assets/logo.png">-->
<!--    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import codemirror from './components/codemirror/codemirror'
export default {
  name: 'app',
  components: {
    codemirror
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
}
  html,body{
    padding: 0px;
    margin: 0px;
  }
</style>

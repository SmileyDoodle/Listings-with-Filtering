<template>
  <div id="app">
    <Header></Header>
    <List></List>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import List from './components/List.vue'

export default {
  name: 'App',
  components: {
    Header,
    List,
  }
}
</script>

<style>
body {
  margin: 0;
}
#app {
  font-family: 'Spartan', sans-serif;
  font-size: 15px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: hsl(180, 52%, 96%);
  margin: 0;
  min-height: 100vh;
  padding-bottom: 5rem;
}
</style>

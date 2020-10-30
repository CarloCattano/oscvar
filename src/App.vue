<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <NodePanel msg="I/O"/>
  </div>
</template>

<script>
import NodePanel from './components/NodePanel.vue'

export default {
  name: 'App',
  components: {
    NodePanel
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
img {
  width: 4%;
}
</style>

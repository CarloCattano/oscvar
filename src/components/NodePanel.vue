<template>
  <div class="nodepanel">
    <h1>{{ msg }}</h1>
    <IO_node v-for="(data, index) in initConf.cv" 
            v-bind:key="data.text" 
            :mindex="index">
    </IO_node>
  </div>
</template>
<script>

import IO_node from './IO_node.vue'
import cv_config from "../cv_config.json"

export default {
  name: 'NodePanel',
  props: {
    msg: String
  },
  data(){
    return{
      initConf: cv_config,
    }
  },
  components:{
    IO_node
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  margin: 0;
  padding: 0;
}

div{
  border-style: solid;
}
h1{
  padding: 0;
  text-align: left;
  margin-left:0;
}
h3 {
  margin: 0px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 0px;
}
a {
  color: #42b983;
}
</style>

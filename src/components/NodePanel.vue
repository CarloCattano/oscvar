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
import axios from 'axios'
const baseURL = "http://localhost:3000/cv"

export default {
  name: 'NodePanel',
  props: {
    msg: String
  },
  data(){
    return{
      initConf: cv_config,
      jsonObject: null,
     
      configData:[]
    }
  },
  components:{
    IO_node
  },
  methods: { //TEst axios post failing
    async addTodo() {
      axios.post('/cv', {
                0: 'Fred',
                1: 'Flintstone'
    })
    .then(function (response) {
      console.log(response);
    })
    .catch(function (error) {
      console.log(error);
    });
    }
  },
  async created(){
    try {
      const res = await axios.get(baseURL)
      this.configData = res.data
      console.log("LOADED DATA FROM SERVER")
     // this.addTodo()   // POST REQUEST TO ADD/MOD DATA ?? 
    } catch(e) {
      console.error(e)
      }
  }
}
</script>
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

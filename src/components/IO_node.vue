<template>
<div id="io_node">
  <p>{{ mindex }}</p>
  <div class="standbyme">
    <vue-dropdown
      :config="config_mode" @setSelectedOption="setNewSelectedOption($event,config_mode);"></vue-dropdown>
  </div>
  <div class="standbyme">
    <vue-dropdown :config="config_range" @setSelectedOption="setNewSelectedOption($event,config_range);">
    </vue-dropdown>
  </div>
    <div class="standbyme">
    <vue-dropdown :config="config_name" @setSelectedOption="setNewSelectedOption($event,config_range);">
    </vue-dropdown>
  </div>
</div>

</template>
<script>
import vueDropdown from "../../node_modules/vue-dynamic-dropdown/dropdown";
import cv_config from "../cv_config.json"

export default {
name: "io_node",
components: {
  vueDropdown
},
props:['mindex'],
data: function() {
  return {
    cvConfigData : cv_config, // READ FROM JSON FILE
    config_mode: {
      options: [
        {
          value: "CV out"
        },
        {
          value: "CV In"
        },
        {
          value: "Digital In"
        }
      ],
      
      placeholder: "Mode",
      backgroundColor: "#cde4f5",
      textColor: "black",
      borderRadius: "1.5em",
      border: "1px solid gray",
      width: 180
    },
    config_range: {
      options: [
        {
          value: "-5 5V"
        },
        {
          value: "0 10V"
        },
        {
          value: "-2 5V"
        }
      ],
      
      placeholder: "Range",
      backgroundColor: "#cde4f5",
      textColor: "black",
      borderRadius: "1.5em",
      border: "1px solid gray",
      width: 180
    },	
    config_name: {
      options: ["Add yours"],
      placeholder: cv_config['cv'][this.mindex]['name'],
      backgroundColor: "#cde4f5",
      textColor: "black",
      borderRadius: "1.5em",
      border: "1px solid gray",
      width: 300
    }
  };
},
created:function() {
  // SET INIT STATE OF EACH NODE WITH RESPECTIVE DATA FROM THE JSON
  var initMode = (this.cvConfigData['cv'][this.mindex]['mode'])   
  var initRange =(this.cvConfigData['cv'][this.mindex]['range'])     

  // DISPLAY LOADED DATA TO LABEL
  this.config_mode.placeholder = this.config_mode.options[initMode].value
  this.config_range.placeholder = this.config_range.options[initRange].value
},

methods: {

  setNewSelectedOption(selectedOption,property) {

    property.placeholder = selectedOption.value
    
    // TO DO send to JSON property with IO index and props 
    // User changes range or mode 
    if(property == this.config_range){
      console.log("INDEX "+ this.mindex + " Range : "+ selectedOption.value)
    }
    if(property == this.config_mode){
      console.log("INDEX "+ this.mindex + "Mode : "+ selectedOption.value)
    }
  }
},
};
</script>
<style>
#io_node {
  border-style: none;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 0.5rem;
  margin-left: 1.2rem;
}

.standbyme {
  text-align: left;
  display: inline-block;
  margin-left: 3rem;
  padding: 0;
}

p {
  font-style: italic;
  text-align: center;
  margin-left: 0.1rem;
  padding: 2%;
  display: inline;
  margin-right: 0;
  font-size: 0.8rem;
  font-weight: 900;
}
</style>

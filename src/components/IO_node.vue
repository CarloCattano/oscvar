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
			cvConfigData : cv_config,
			config_mode: {
				options: [
					{
						value: "Digital In"
					},
					{
						value: "CV In"
					},
					{
						value: "CV out"
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
				placeholder: cv_config['cv'][this.mindex-1]['name'],
				backgroundColor: "#cde4f5",
				textColor: "black",
				borderRadius: "1.5em",
				border: "1px solid gray",
				width: 300
			}
		};
	},
	created:function() {
		console.log(this.cvConfigData)     
		var ioType = this.cvConfigData['cv'][this.mindex-1]['name']      
		console.log("IO TYPE " + ioType)

		if(ioType == 'cv_input'){
			this.config_mode.placeholder = 0
		}

		console.log(this.config_mode.options[0].value + " THIS CONFIG MODE")
	},
	methods: {
		setNewSelectedOption(selectedOption,property) {
			property.placeholder = selectedOption.value
			// TO DO send to JSON property with IO index and props 
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

	font-family: "Avenir", Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: left;
	color: #2c3e50;
	margin-top: 0.5rem;
}

.standbyme {
	text-align: left;
	display: inline-block;
}
p{
	margin: 0;
	padding: 0%;
	display: inline;
	margin-right: 0.4rem;
}
</style>

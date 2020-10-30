<template>
	<div id="io_node">
		<p>{{ index }}</p>
		<div class="standbyme">
		<vue-dropdown
			:config="config_mode"
			@setSelectedOption="setNewSelectedOption($event,config_mode);"></vue-dropdown>
		</div>
		<div class="standbyme">
		<vue-dropdown
			:config="config_range"
			@setSelectedOption="setNewSelectedOption($event,config_range);"></vue-dropdown>
		</div>
	</div>
</template>
<script>

import vueDropdown from "../../node_modules/vue-dynamic-dropdown/dropdown";

export default {
	name: "io_node",
	components: {
		vueDropdown
	},
	props:{
		index: -1,
	},

	data: function() {
		return {
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
			}	
		};
	},

	methods: {
		setNewSelectedOption(selectedOption,property) {
			property.placeholder = selectedOption.value
												
			// TO DO send to JSON property with IO index and props 
			if(property == this.config_range){
				console.log("Range : "+ selectedOption.value)
			}
			if(property == this.config_mode){
				console.log("Mode : "+ selectedOption.value)
			}
		}
	}
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

</style>

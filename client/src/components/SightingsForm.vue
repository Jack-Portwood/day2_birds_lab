<template lang="html">
	<form id="sightings-form" v-on:submit="sightingAdded" method="post">
		<h2>Add a Sighting</h2>
		<div class="formWrap">
			<label for="species">Species:</label>
			<input type="text" v-model="species" id="species" />
		</div>
		<div class="formWrap">
			<label for="location">Location:</label>
			<input type="text" v-model="location"  id="location" />
		</div>
		<div class="formWrap">
			<label for="date">Date:</label>
			<input type="date" v-model="date"  id="date" />
		</div>

		<input type="submit" value="Save" id="save"/>
	</form>
</template>

<script>
import { eventBus} from '@/main.js'
import SightingService from '@/services/SightingService.js'
export default {
	name: "sightings-form",
	data(){
		return {
			species: '',
			location: '',
			date: null

		}
	},
	methods: {
		sightingAdded: function(e) {
			e.preventDefault()
			const sighting ={
				species: this.species,
				location: this.location,
				date: this.date 
			}
		
			SightingService.postSighting(sighting)
				.then(res => eventBus.$emit('sighting-added',res))
		}
	} 
}

		

		
			// WHAT DO WE WANT TO DO HERE?
			//	1) Prevent default on the form

			//	2) Create a new "sighting" object from the form data
			//	3) POST this new "sighting" object to the server project
			// 		so that it saves in DB
			//	4) $emit the server response (which will include ID) on
			// 		eventBus so that the client side will show us the new bird
			
				
</script>

<style lang="css" scoped>
h2 {
	margin: 10px 0;
	padding: 0;
}

form {
	width: 75%;
	margin: 0 auto;
	background: rgba(255, 255, 255, 0.7);
	padding: 20px;
	margin-bottom: 40px;
}

label {
	min-width: 100px;
	display: inline-block;
}

.formWrap {
	margin-bottom: 10px;
}
</style>

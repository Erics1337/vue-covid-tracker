<template>
	<div class="home">Hello World</div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/Header.vue'

export default {
	name: 'HomeView',
	components: {},
	methods: {
		async fetchCovidData() {
			const response = await fetch('https://covid19api.com/summary')
			const data = await response.json()
			console.log(data)
		},
	},
	async created() {
		const data = await this.fetchCovidData()
		console.log(data)
	},
}
</script>

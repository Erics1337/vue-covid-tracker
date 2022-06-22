<template>
	<main v-if="!loading" class="home">show data</main>
	<main v-else class="flex flex-col align-center justify-center text-center">
		<div class="text-gray-500 text-3xl mt-10 mb-6">Fetching Data</div>
		<img :src="loadingImage" alt="loading" class="w-24 m-auto" />
	</main>
</template>

<script>
// @ is an alias to /src

export default {
	name: 'HomeView',
	components: {},
	data() {
		return {
			loading: true,
			title: 'Global',
			dataData: '',
			status: {},
			countries: [],
			loadingImage: require('../assets/spinning-loading.gif'),
		}
	},
	methods: {
		async fetchCovidData() {
			const response = await fetch('https://covid19api.com/summary')
			const data = await response.json()
			return data
		},
	},
	async created() {
		const data = await this.fetchCovidData()
		this.dataDate = data.Date
		this.stats = data.Global
		this.countries = data.Countries
		this.loading = false
	},
}
</script>

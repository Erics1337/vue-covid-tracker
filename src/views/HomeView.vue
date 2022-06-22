<template>
	<main v-if="!loading" class="home">
		<DataTitle :text="title" :dataDate="dataDate" />
		<DataBoxes :stats="stats" />
	</main>
	<main v-else class="flex flex-col align-center justify-center text-center">
		<div class="text-gray-500 text-3xl mt-10 mb-6">Fetching Data</div>
		<img :src="loadingImage" alt="loading" class="w-24 m-auto" />
	</main>
</template>

<script>
// @ is an alias to /src
import DataTitle from '@/components/DataTitle'
import DataBoxes from '@/components/DataBoxes'

export default {
	name: 'HomeView',
	components: { DataTitle, DataBoxes },
	data() {
		return {
			loading: true,
			title: 'Global',
			dataDate: '',
			status: {},
			countries: [],
			loadingImage: require('../assets/spinning-loading.gif'),
		}
	},
	methods: {
		async fetchCovidData() {
			const response = await fetch('https://api.covid19api.com/summary')
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

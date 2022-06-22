<template>
	<main v-if="!loading" class="home">
		<DataTitle :text="title" :dataDate="dataDate" />
		<DataBoxes :stats="stats" />
		<CountrySelect
			@country-changed="getCountryData"
			:countries="countries"
		/>
		<button
			@click="getGlobalData"
			v-if="stats"
			class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600"
		>
			Clear Country
		</button>
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
import CountrySelect from '@/components/CountrySelect'

export default {
	name: 'HomeView',
	components: { DataTitle, DataBoxes, CountrySelect },
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
		async getCountryData(country) {
			this.stats = country
			this.title = country.Country
		},
		async getGlobalData() {
			this.loading = true
			const data = await this.fetchCovidData()
			this.stats = data.Global
			this.title = 'Global'
			this.loading = false
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

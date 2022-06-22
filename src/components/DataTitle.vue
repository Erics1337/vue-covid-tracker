<template>
	<div class="text-center">
		<h2 class="font-bold text-3xl">{{ text }}</h2>
		<div class="text-2xl mt-4 bg-10">
			{{ timestamp }}
		</div>
	</div>
</template>

<script>
import moment from 'moment'

export default {
	name: 'DataTitle',
	props: {
		text: {
			type: String,
			required: true,
		},
		dataDate: {
			type: String,
			required: true,
		},
	},
	computed: {
		formattedDate() {
			return moment(this.dataDate).format('MMMM Do YYYY, h:mm:ss a')
		},
	},
}
</script>

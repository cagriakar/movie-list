<template>
	<v-container>
		<v-card>
			<v-card-title>
				Movies
				<v-spacer></v-spacer>
				<v-text-field
					v-model="search"
					append-icon="mdi-magnify"
					label="Search"
					single-line
					hide-details
				></v-text-field>
			</v-card-title>
			<v-data-table
				:headers="headers"
				:items="infos"
				:search="search"
				multi-sort
			
			>
				<template #item.release_date="{item}">
					{{ new Date(item.release_date).getFullYear() }}
				</template>
				<template #item.original_language="{item}">
					{{ item.original_language.toUpperCase() }}
				</template>
			</v-data-table>
		</v-card>
	</v-container>
</template>

<script>
import axios from 'axios';

const url =
	'https://api.themoviedb.org/3/discover/movie?api_key=733cf72960e3837a08ca59c1fbbc84ac&language=en-US&sort_by=popularity.desc&page=1';

async function getData() {
	const response = await axios.get(url);
	const {data: {results}} = response
	return results
}

export default {
	name: 'TableComponent',
	data() {
		return {
			search: '',
			infos: []
		};
	},
	computed: {
		headers() {
			return [
				{ text: 'ID', value: 'id' },
				{ text: 'Name', value: 'title' },
				{ text: 'Point', value: 'vote_average' },
				{ text: 'Release Date', value: 'release_date' },
				{ text: 'Popularity', value: 'popularity' },
				{ text: 'Original Language', value: 'original_language' }
			];
		}
	},
	beforeMount () {
		this.getAllData()
	},
	methods: {
		async getAllData() {
			const response = await getData()
			this.infos = [...response]
		}
	}
};
</script>

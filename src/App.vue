<template>
	<div>
		<TableComponent />
	</div>
</template>

<script>
import TableComponent from './components/TableComponent';

// TODO: https://api.themoviedb.org/3/discover/movie?api_key=733cf72960e3837a08ca59c1fbbc84ac&language=en-US&sort_by=popularity.desc&page=1
export default {
	name: 'App',
	components: {
		TableComponent
	}
};
</script>

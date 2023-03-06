<template>
	<body>
		<Header/> 
		<router-view :table='table'></router-view>
	</body>
</template>

<script>
import Header from './components/Header.vue'

export default {
	name: 'App',
	components: {
		Header,
	},
	data(){
		return{
		table:[],
		}
	},
	methods:{
		async fetchTable(){
			const res = await fetch('http://localhost:5000/table')
			const data = await res.json()
			return data
		},
	},
	async created(){
		this.table = await this.fetchTable()
	}  
}
</script>

<style>
	*{
		margin: 0;
		padding: 0;
		box-sizing: border-box;
		/* border: 1px solid green; */
	}
	body{
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
	}
</style>

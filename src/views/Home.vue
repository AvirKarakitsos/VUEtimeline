<template>
    <main>
		<i @click="goBack()" class="fas fa-chevron-circle-left" id="back"></i>
		<div class="menu">
			<Canvas :table="table" :cpt="cpt"/>
			<Sectionlist :table="table" :cpt="cpt"/>
		</div>
		<i @click="goNext()" class="fas fa-chevron-circle-right " id="next"></i>
    </main>
	<ul>
		<li v-for="ligne in tableFilter" :key="ligne.id">
			<div class="color-bg" :style="'background-color:'+ligne.couleur"></div>{{ " "+ligne.pays }}
		</li>
	</ul>
	<section>
		<p>La collection de livres <strong>Les génies des mathématiques</strong> a été publiée entre 2018 et 2019 par « Le Monde », en collaboration avec « L’Obs ». Elle propose la biographie de soixante mathématiciens (dont trois femmes) de l'antiquité jusqu'au XXème siecle. Une façon différnte de raconter les mathématiques où le contexte historique permet de mieux comprendre les travaux de recherches du mathématicien. Un format agréable dont les livres font environ 150 pages rend la lecture accessible à nimporte quel amateur d'histoire et de mathématiques.<br/><br/>La frise chronologique représente les soixante mathématiciens abordés dans la collection au cours du temps. Vous pouvez cliquer sur un  nom pour voir sa fiche récapitulative. <span class="italique">En savoir plus</span> vous amène sur une page avec la couverture du livre et son résumé.</p>
	</section>
</template>

<script>
import Canvas from '../components/Canvas.vue'
import Sectionlist from '../components/Sectionlist.vue'

export default {
	name: 'Home',
	props:["table"],
	components: {
		Canvas,
		Sectionlist,
	},
	data(){
		return{
		cpt:0,
		tableFilter:[]
		}
	},
	methods:{
		goNext(){
			if(this.cpt<5){
				this.cpt++
				if(this.cpt == 5){
					document.getElementById("next").style.color = "#EBECF0";
					document.getElementById("next").style.cursor = "auto";
				}
				document.getElementById("back").style.color = "black";
				document.getElementById("back").style.cursor = "pointer";
			}
		},
		goBack(){
			if(this.cpt>0){
				this.cpt--
				if(this.cpt == 0){
					document.getElementById("back").style.color = "#EBECF0";
					document.getElementById("back").style.cursor = "auto";
				}
				document.getElementById("next").style.color = "black";
				document.getElementById("next").style.cursor = "pointer";
			}
		},
		async fetchTable(){
			const res = await fetch('http://localhost:5000/table')
			const data = await res.json()
			return data
		},
	},
	async created(){
		let tab2 =[]
		const tab= await this.fetchTable()
		tab.map(val => {
			if((!tab2.includes(val.couleur)) && (val.couleur !== "")){
				tab2.push(val.couleur)
				this.tableFilter.push(val)
			}
		})
	}
}
</script>

<style scoped>
	main{
		height: 125px;
		width: 1100px;
		margin: 5rem auto 0 auto;
		display: flex;
		justify-content: space-between;
	}
	#back{
		font-size: 2.2rem;
		color: #EBECF0;
		cursor: auto;
	}
	#next{
		font-size: 2.2rem;
		color: black;
		cursor: pointer;
	}

	ul{
		width: 300px;
		margin-left: 12rem;
		padding: .5rem 1rem;
		-webkit-column-count: 2;  /* Chrome/Opera, Safari */
		-moz-column-count: 2; /* Mozilla Firefox */
		column-count: 2;
		list-style-type: none;
		border: 2px solid black;
	}
	.color-bg{
		height: 20px;
		width: 25px;
		margin: 4px 4px 0 0;
		display: inline-block;
	}

	section{
		width: 550px;
		margin: 0 auto;
		padding-top: 0.5rem;
		text-align: justify;
		box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);
	}
	.italique{
		font-style: italic;
	}
</style>

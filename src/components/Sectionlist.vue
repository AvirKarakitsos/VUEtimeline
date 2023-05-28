<template>
    <section class="timeline" v-if="cpt>=1">
        <div v-for="ligne in table.filter(val => (val.date>date_inf(cpt))&&(val.date<date_sup(cpt)))" :key="ligne.id">
            
            <div @click="afficher(ligne.id)" 
            :class="[ligne.id%2==0 ? 'paire' : 'impaire', 'libelle']"
            class="box"
            :id="'titre'+ligne.id"
            :style="'background-color:'+ligne.couleur"
            v-if="(ligne.id<=30)||(ligne.id>=59)">

                <h5>{{ligne.nom}}</h5>
            
            </div>

            <div @click="afficher(ligne.id)" 
            :class="[ligne.id%2==0 ? 'paire' : 'impaire', 'autre']"
            :id="'titre'+ligne.id"
            :style="'background-color:'+ligne.couleur"
            v-if="((ligne.id>30)&&(ligne.id<54))||((ligne.id>54)&&(ligne.id<=58))"
            @mouseover="mouseover(ligne.id)"
            @mouseleave="mouseleave(ligne.id)">

                 <h5>{{ligne.nom}}</h5>
            
            </div>
        </div>
    </section>
    <section class="timeline" v-else-if="cpt==0">
        <div v-for="ligne in table.filter(val => val.id <= 10)" :key="ligne.id">
            
            <div @click="afficher(ligne.id)" 
            :class="[ligne.id%2==0 ? 'paire' : 'impaire', 'libelle']"
            :id="'titre'+ligne.id"
            :style="'background-color:'+ligne.couleur">

                <h5>{{ligne.nom}}</h5>
            
            </div>
        </div>
    </section>
    <div class="articles" v-show="hidden">
        <Description :afficherId="afficherId" @changer="change"/>
    </div>
</template>

<script>
import Description from './Description'
export default{
    name:'Sectionlist',
    props:["table","cpt"],
    components:{
        Description
    },
    data(){
        return{
            afficherId:[],
            hidden:false,
        }
    },
    methods:{
        change(index){
            this.hidden= index
        },
        afficher(index){
            this.afficherId=this.table.filter(val => val.id==index)
            this.hidden=true
        },
        date_inf(input){
            return 1500+(input-1)*100
        },
        date_sup(input){
            return 1500+input*100
        },
        mouseover(input){
            let selected = null
            selected = document.getElementById(`titre${input}`)
            selected.classList.add('hover')
            selected.style.zIndex = 10
        },
        mouseleave(input){
            let selected = null
            selected = document.getElementById(`titre${input}`)
            selected.classList.remove('hover')
            selected.style.zIndex = 0
        },
    }
}
</script>
    
<style scoped>
    @import '../assets/css/style.css';
</style>
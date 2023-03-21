<template>
    <section v-for="ligne in afficherId" :key="ligne.id">
        <div>
            <p align="center"><strong>{{ligne.prenom+' '+ligne.nom}}</strong></p><br/>    
            <p>Année de naissance : <b>{{ligne.date}}</b></p>
            <p>Pays de naissance : <b>{{ligne.pays}}</b></p><br/>
            <router-link :to="{name:'About', params:{nom: ligne.nom}}">En savoir plus</router-link>
        </div>
        <div class="close">
            <i @click="$emit('changer',cacher)" class="fas fa-times-circle"></i>
        </div>
    </section>
</template>

<script>
export default {
    name:"Description",
    props:["afficherId"],
    emits:["changer"],
    data(){
        return{
            cacher:false
        }
    },
}
</script>
<style scoped>
    section{
        height: 150px;
        width: 300px;
        margin: 3rem auto 0 auto;
        padding: 1.3rem;
        display: flex;
        justify-content: space-between;
        border-radius: 10px;
        box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
    }
    .close{
        font-size: 1.5rem;
        cursor: pointer; 
        color: black;    
    }
</style>
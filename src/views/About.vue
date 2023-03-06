<template>
    <section v-for="ligne in table.filter(val => val.nom === nom)" :key="ligne.id"> 
        <img :src="getImgUrl(ligne.nom)" alt="">
        <div>
            <p>{{ligne.content}}</p><br/>
            <router-link :to="{name:'Home'}">Page d'accueil</router-link>
        </div>
	</section>
</template>

<script>
export default {
    props:['nom','table'],
    methods:{
          getImgUrl(input) {
            let val = input.toLowerCase()
            let images = require.context('../assets/images/collection/', false,/\.jpg$/)
            return images( './'+val + ".jpg")
        },
    }
}
</script>

<style scoped>
    section{
        height: 500px;
        width: 850px;
        margin: 2.5rem auto;
        display: flex;
        justify-content: space-between;
    }
    img{
        width: 400px;
        object-fit: scale-down;   
    }
    div{
        width: 400px;
        padding: 3rem;
        text-align: justify;
        line-height: 1.5rem;
        border-radius: 10px;
        box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
    }

    @media all and (max-width: 1200px){
        section{
            display: block;
            text-align: center;
        }
        div{
            margin: 3rem auto;
    }
    }
</style>

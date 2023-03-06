<template>
	<nav>
		<img src="../assets/logo.png" alt="" onclick='location.reload()'/>
		<h4>Vue JS</h4>
	</nav>
</template>

<script>
export default {
  name: 'Header'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  nav{
	height: 4rem;
	display: flex;
	align-items: center;
	border-bottom: 1px solid rgb(243 244 246);
    background-color: white;
  }
  img{
	height: 3rem;
	width: 3rem;
	position: relative;
	left: 10%;
	cursor: pointer;
  }
  h4{
	position: relative;
	left: 11%;
	font-size: 0.8rem;
	color: rgb(31 41 55);
  }
</style>

<template>
  <div id="app">
			<myHeader></myHeader>
			
			<tab></tab>
   
			
  </div>
</template>

<script>
	import myHeader from './components/header/header.vue';
	import tab from './components/tab.vue';

export default {
  name: 'App',
	data(){
		return {}
	},
	components:{
		myHeader,tab
	}
};
</script>

<style>
	body,html{
		margin: 0px;
		padding: 0px;
		width: 100%;
		height: 100%;
		list-style: none;
	}
	a{
		text-decoration: none;
	}
	#app{
		width: 100%;
		height: 100%;
	}
</style>

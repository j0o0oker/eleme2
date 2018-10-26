<template>
	<div class="star">
		<div class="star-wrapper">
			<img width="12" height="12" src="../assets/images/astar.png" alt="" v-show="score>=1">
			<img width="12" height="12" src="../assets/images/astar.png" alt="" v-show="score>=2">
			<img width="12" height="12" src="../assets/images/astar.png" alt="" v-show="score>=3">
			<img width="12" height="12" src="../assets/images/astar.png" alt="" v-show="score>=4">
			<img width="12" height="12" src="../assets/images/astar.png" alt="" v-show="score>=5">
			<img width="12" height="12" src="../assets/images/halfstar.png" alt="" v-show="parseInt(score)!==score">
		</div>
	</div>
</template>
<script>
	export default{
		data(){
			return {msg:'collect'}
		},
		props: {
			score: {
				type: Number,
				default:0
			}
		},
		created(){
			
		},
		methods:{
			
		},
		computed:{},
		components:{}
	}
</script>
<style scoped>
	.star-wrapper {
		display: inline-block;
	}
</style>

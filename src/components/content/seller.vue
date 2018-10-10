<template>
	<div>
		<slot></slot>
		<div class="content">
			12
		</div>
	</div>
</template>
<script>
	export default{
		data(){
			return {msg:'collect'}
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
	.content{
		position: fixed;
		top:7;
		bottom: 10%;
		width: 100%;
		height: 58%;
		background-color: #9ACD32;
	}
</style>

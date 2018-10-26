<template>
	<div class="tab-container">
		
		<router-view></router-view>
		<router-link class="tab router-link-active" to="goods">商品</router-link>
		<router-link class="tab" to="ratings">评论</router-link>
		<router-link class="tab" to="seller">商家</router-link>
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
	.router-link-active{
		color: #FF0000;
	}
	.tab-container{
		display: flex;
		width: 100%;
		height: 40px;
		background-color:#fff;
		cursor: pointer;
		
	}
	.tab-container .tab{
		display: flex;
		flex-direction:row;
		align-items: center;
		justify-content: center;
		flex: 1;
		color: rgb(77,85,93);
		font-size: 14px;
		font-weight: 200;
		transition:all 2s;
		font-size: 14px;
	}
	.tab-container .tab:hover{
		color:red;
	}
</style>

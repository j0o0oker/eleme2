<template>
	<div class="tab-container">
		
		<router-view></router-view>
		<router-link class="tab router-link-active" to="goods">商品</router-link>
		<router-link class="tab" to="seller">评论</router-link>
		<router-link class="tab" to="ratings">商家</router-link>
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
		height: 7%;
		background-color: antiquewhite;
		cursor: pointer;
		
	}
	.tab-container .tab{
		display: flex;
		flex-direction:row;
		align-items: center;
		justify-content: center;
		flex: 1;
		color: yellowgreen;
		font-size: 21px;
		font-weight: 100;
		transition:all 2s;
	}
	.tab-container .tab:hover{
		color:red;
	}
</style>

<template>
	<div class="shopcart">
			<div class="content-left">
				<div class="logo-container">
					<div class="logo-wrapper">
						<div class="logo">
							<img width="30" height="30" src="../../assets/images/gcw.png" alt="">
						</div>
					</div>
				</div>
				<div class="price">$0</div>
				<div class="description">qq</div>
			</div>
			<div class="content-right">起送</div>
	</div>
</template>
<script>
	export default{
		data(){
			return {msg:''}
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
	.shopcart{
		display: flex;
		position: fixed;
		left:0;
		bottom:0;
		z-index: 10;
		width: 100%;
		height: 7%;
		background-color: #363636;
	}
	.shopcart .content-left{
		flex:  0 0 275px;
		height: 100%;
		
	}
	.shopcart .content-left .logo-container{
		position: absolute;
		left: 5%;
		top: -30%;
		width: 50px;
		height: 50px;
		border-radius: 50%;
		overflow: hidden;
		background-color: #000;
	}
	.shopcart .content-left .logo-wrapper{
		position: relative;
		left: 5px;
		top: 5px;
		width: 40px;
		height: 40px;
		border-radius: 50%;
		overflow: hidden;
		background-color: #fff;
		
	}
	
	.shopcart .content-left .logo-wrapper .logo{
		width:30px;
		height: 30px;
		border-radius: 50%;
		overflow: hidden;
		position: relative;
		top: 5px;
		left: 5px;
	}
	.shopcart .content-left .price{
		position: absolute;
		left: 25%;
		width: 50px;
		height: 100%;
		color: #F3F5F7;
		font-size: 22px;
		line-height: 46px;
	}
	.shopcart .content-left .description{
		position: absolute;
		left: 50%;
		height: 100%;
		color: #F3F5F7;
		font-size: 22px;
		line-height: 46px;
	}
	.shopcart .content-right{
		flex:1;
		height: 100%;
		color: #F3F5F7;
		font-size: 22px;
		line-height: 46px;
		text-align: center;
	}
</style>

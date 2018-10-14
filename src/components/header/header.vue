<template>
	<div class="container">
		<div class="bg"></div>
		<div class="content-wrapper">
			<div class="avatar">
				<img  width="64" height="64" :src="seller.avatar">
			</div>
			<div class="content">
				<div class="title">
					<span class="brand">
						<img width="27" height="22" src="./brand@2x.png" alt="">
					</span>
					<span class="name">{{seller.name}}</span>
				</div>
				<div class="description">{{seller.description}}/{{seller.deliveryTime}}</div>
				<div class="support" @click="truth=!truth">
					<span class="icon">
						<img width="16" height="16" src="./decrease_2@2x.png" alt="">
					</span>
					<span class="text" v-if="seller.supports">{{seller.supports[0].description}}</span>
					<span class="supportNum">{{seller.supports.length}}ä¸</span>
				</div>
					
			</div>
		</div>
			
		<div class="bulletin-wrapper">
			<span class="icon">
				<img width="27" height="14" src="./bulletin@2x.png" alt="">
			</span>
			<span class="text">{{seller.bulletin}}</span>
			<i class="arrow">></i>
		</div>
		<div class="modal" v-show="truth">
			<div class="close" @click="truth=!truth">x</div>
		</div>
	</div>
</template>
<script>
	export default{
		
		data() {
			return {
				truth:false,
				seller: {}
			};
		},
		created(){
			console.log(this.sellerss);
		},
		created() {
			this.$http({
				methos:'get',
				url:'api/seller'
				
			}).then(res => {
				
				this.seller = res.data.data;
				
				
			},res => {
				alert('err');
			})
		},
		methods:{
			
		}
	}
</script>
<style scoped>
	.container{
		position: fixed;
		left: 0;
		top: 0;
		width:100%;
		height:25%;
		color: #fff;
		background:rgba(7,17,27,0.8);
		z-index: 1;
		font-weight: 200;
		overflow: hidden;
	}
	.container .bg{
		background-repeat: no-repeat;
		background-size: cover;
		background: url(http://static.galileo.xiaojukeji.com/static/tms/seller_avatar_256px.jpg);
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		left: 0;
		z-index: -1;
		filter: blur(20px);
	}
	.content-wrapper{
		display: flex;
		position: absolute;
		width: 80%;
		height:62%;
		left: 10%;
		top: 18%;
		font-size: 0;
		
		
	}
	.content-wrapper .avatar{
		flex: 0 0 64px;
		display: inline-block;
		
		top: 0;
	}
	.content-wrapper .content{
		flex: 1;
		display: inline-block;
		margin-left: 16px;
		
	}
	.content-wrapper .content .title{
		margin: 02px 0 8px 24px;
		font-size: 17px;
		line-height: 17px;
		
	}
	.content-wrapper .content .title .brand {
		display: inline-block;
		vertical-align: top;
		
	}
	.content-wrapper .content .title .name{
		vertical-align: top;
		
	}
	.content-wrapper .content .description{
		margin: 02px 0 8px 24px;
		font-size: 12px;
	}
	.content-wrapper .content .support{
		margin: 02px 0 8px 24px;
		font-size: 12px;
		line-height: 12px;
		

		
	}
	.content-wrapper .content .support .icon{
		display: inline-block;
		vertical-align: top;
		width: 15px;
		height: 15px;
	}
	.content-wrapper .content .support .text{
		vertical-align: top;
		line-height: 16px;
	}
	.content-wrapper .content .support .supportNum{
		display: inline-block;
		position: absolute;
		right: 0;
		width: 30px;
		height: 12px;
		text-align: center;
		border-radius: 30%;
		font-size: 12px;
		line-height: 12px;
		background-color: rgba(0,0,0,0.2);
	}
	.bulletin-wrapper{
		
		position: absolute;
		width: 100%;
		height:28px;
		line-height: 28px;
	
		top: 80%;
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
		font-size: 10px;
		background-color: rgba(7,17,27,0.2);
		
	}
	.bulletin-wrapper .icon{
		display: inline-block;
		vertical-align: middle;
		height: 14px;
		transform: translateY(-50%);
	}
	.bulletin-wrapper .text{
		
		line-height: 14px;
		
	}
	.bulletin-wrapper .arrow{
		vertical-align: top;
		position: fixed;
		top: 18%;
		left:86%;
	}
	.container .modal{
		position: fixed;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		background-color: rgba(7,17,27,0.8);
	}
	.container .modal .close{
		position: absolute;
		bottom: 10px;
		left: 50%;
		transform: translateX(-50%);
		width: 50px;
		height: 50px;
		border: 1px solid rgba(255,255,255,0.2);
		border-radius: 50%;
		line-height: 44px;
		font-size: 40px;
		text-align: center;
		color: #fff;
		transition: all 2s;
		overflow: scroll;
	}
	.container .modal .close:hover{
		border: 1px solid rgba(255,255,255,0.8);
		cursor: pointer;
	}
	
</style>

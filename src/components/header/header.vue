<template>
	<div class="container">
		<div class="bg"></div>
		<div class="content-wrapper"  @click="truth=!truth">
			<div class="avatar">
				<img  width="64" height="64" :src="seller.avatar">
			</div>
			<div class="content">
				<div class="title">
					<span class="brand">
						<img width="16" height="16" src="./brand@2x.png" alt="">
					</span>
					<span class="name">{{seller.name}}</span>
				</div>
				<div class="description">{{seller.description}}/{{seller.deliveryTime}}分钟送达</div>
				<div class="support" v-if="seller.supports">
					<span class="icon">
						<img width="10" height="10" src="./decrease_2@2x.png" alt="">
					</span>
					<span class="text">{{seller.supports[0].description}}</span>
					<span class="supportNum">{{seller.supports.length}}涓</span>
				</div>
					
			</div>
		</div>
			
		<div class="bulletin-wrapper">
			<span class="icon">
				<img width="27" height="12" src="./bulletin@2x.png" alt="">
			</span>
			<span class="text">{{seller.bulletin}}</span>
			<i class="arrow">></i>
		</div>
		<div class="modal" v-show="truth" ref="modalhock">
			<div>
				<div class="title">{{seller.name}}</div>
				<div class="star">
					<star :score="seller.score"></star>
				</div>
				<div class="discount-info">
					<span class="title">优惠信息</span>
					<div class="discounts">
						<ul>
							<li class="discount" v-for="item in seller.supports">{{item.description}}</li>
						</ul>
					</div>
				</div>
				<div class="seller-announcement">
					<span class="title">商家公告</span>
					<p>{{seller.bulletin}}</p>
				</div>
				<div class="close" @click="truth=!truth">x</div>
			</div>
		</div>
	</div>
</template>
<script>
	import star from '../star.vue';
	import BScroll from 'better-scroll';
	export default{
		data() {
			return {
				truth:false,
				seller: {}
			};
		},
		updated() {
			this._modalScroll();
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
			
			_modalScroll() {
				console.log(2)
				let scroll = new BScroll(this.$refs.modalhock,{
					probeType:3,click:true,taps:true

				})
			}
		},
		components: {
			star
		}
	}
</script>
<style scoped>
	.container{
		height: auto;
		padding-top: 24px;
		cursor: pointer;
		background-color: rgba(7,17,27,0.5);
	}
	.container .bg{
		background-repeat: no-repeat;
		background-size: cover;
		background: url(http://static.galileo.xiaojukeji.com/static/tms/seller_avatar_256px.jpg);
		position: absolute;
		width: 100%;
		height: 20%;
		top: 0;
		left: 0;
		z-index: -1;
		filter: blur(6px);
	}
	.content-wrapper{
		display: flex;
		margin: 0 12px 18px 24px;
	}
	.content-wrapper .avatar{
		flex: 0 0 80px;
	}
	.content-wrapper .content{
		flex: 1;
	}
	.content-wrapper .content .title{
		
	}
	.content-wrapper .content .title .brand {
		
	}
	.content-wrapper .content .title .name{
		display: inline-block;
		margin-left: 6px;
		font-size: 16px;
		color: #fff;
	}
	.content-wrapper .content .description{
		display: inline-block;
		margin-top: 8px;
		font-size: 12px;
		color: rgb(147,153,159);
	}
	.content-wrapper .content .support{
		
	}
	.content-wrapper .content .support .icon{
		
	}
	.content-wrapper .content .support .text{
		display: inline-block;
		margin-top: 8px;
		font-size: 10px;
		color: rgb(147,153,159);
	}
	.content-wrapper .content .support .supportNum{
		display: inline-block;
		width: 25px;
		margin-left: 121px;
		border-radius: 10px;
		text-align: center;
		font-size: 10px;
		color: rgb(147,153,159);
		background-color: rgba(7,17,27,0.2);
		

	}
	.bulletin-wrapper{
		background-color: rgba(7,17,27,0.2);
		height: 18px;
		
		
		
	}
	.bulletin-wrapper .icon{
		
	}
	.bulletin-wrapper .text{
		display: inline-block;
		width: 318px;
		height: 10px;
		margin: 4px;
		font-size: 10px;
		color: rgb(147,153,159);
		overflow: hidden;
		text-overflow: ellipsis;
		
		
		
	}
	.bulletin-wrapper .arrow{
		
	}
	.container .modal{
		position: fixed;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		background-color: rgba(7,17,27,0.8);
		z-index: 99;
		overflow: hidden;
	}
	.container .modal .title{
		width: 100%;
		
		margin-top: 64px;
		margin-bottom: 16px;
		text-align: center;
		line-height: 16px;
		font-size: 16px;
		font-weight: 700;
		color: #fff;
	}
	.container .modal .star{
		width: 100%;
		margin-bottom: 27px;
		text-align: center;
	}
	.container .modal .discount-info {
		
	}
	.container .modal .discount-info .title {
		display: inline-block;
		font-size: 14px;
		text-align: center;
		color: #fff;
	}
	.container .modal .discount-info .discounts {
		margin-top: 24px;
		margin-left: 48px;
		
	} 
	.container .modal .discount-info .discounts .discount {
		
		font-size: 12px;
		line-height: 24px;
		color: #f3f5f7;
		list-style: none;
	}
	.container .modal .seller-announcement {
		margin-top: 18px;
		margin-left: 48px;
		margin-right: 48px;
		margin-bottom: 74px;
		
	}
	.container .modal .seller-announcement .title {
		display: inline-block;
		font-size: 14px;
		text-align: center;
		color: #fff;
	}
	.container .modal .seller-announcement p {
		display: inline-block;
		height: 300px;
		margin-top: 24px;
		font-size: 12px;
		line-height: 24px;
		
		color: #f3f5f7;
	}
	.container .modal .close{
		position: absolute;
		bottom: 10px;
		left: 50%;
		width: 50px;
		height: 50px;
		transform: translateX(-50%);
		border: 1px solid rgba(255,255,255,0.2);
		border-radius: 50%;
		line-height: 44px;
		font-size: 40px;
		text-align: center;
		color: #fff;
		overflow: scroll;
		transition: all 2s;
	}
	.container .modal .close:hover{
		border: 1px solid rgba(255,255,255,0.8);
		cursor: pointer;
	}
	
</style>

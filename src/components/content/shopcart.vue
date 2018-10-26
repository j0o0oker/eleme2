<template>
	<div class="shopcart">
			<div class="content-left"  @click="detailShow=!detailShow">
				<div class="logo-container">
					<div class="logo-wrapper">
						<div class="logo">
							<img width="30" height="30" src="../../assets/images/gcw.png" alt="">
						</div>
						<div class="count" v-show="selectFoods.length!==0">{{totalCount}}</div>
					</div>
				</div>
				<div class="price">${{totalPrice}}</div>
				<div class="description">另需配送费{{deliveryPrice}}元</div>
			</div>
			<div class="content-right" @click="detailShow=!detailShow">
				<div class="pay" :class="{toGreen:totalPrice>minPrice}">
					{{payDesc}}
				</div>
			</div>
			<div class="detail" v-show="detailShow">
				<div class="class-header">
					<div class="title">购物车</div>
					<div class="empit" @click="removeCount">清空</div>
				</div>
				<div class="list-content" ref="foodlist">
					<ul>
						<li class="food" v-for="food in selectFoods">
							<span class="name">{{food.name}}</span>
							<div class="price">
								<span>${{food.price*food.count}}</span>
							</div>
							<div class="cartctrl">
								<cartCtrl :food="food"></cartCtrl>
							</div>
						</li>
					</ul>
				</div>
			</div>
	</div>
</template>
<script>
	import BScroll from 'better-scroll';

	import cartCtrl from './cartCtrl.vue';

	export default{
		updated() {
			this.toScroll();
		},
		data() {
			return {
				detailShow:false
			}
		},
		props:{
			deliveryPrice:{
				type:Number,
				default:0
			},
			minPrice:{
				type:Number,
				default:0
			},
			selectFoods:{
				type:Array,
				default() {
					return []
				}
			},
			num:{
				type:Number,
				default:0
			}
		},
		created(){
			
		},
		methods:{
			removeCount() {
				this.selectFoods.forEach((food) => {
					food.count = 0;
				});
				this.detailShow = !this.detailShow;
			},
			toScroll() {
				let scroll = new BScroll(this.$refs.foodlist,{
					probeType:3,click:true,taps:true

				})
			}
		},
		computed:{
			totalPrice() {
				let total = 0;
				this.selectFoods.forEach((food)=>{
					total +=food.price*food.count
				});
				return total
			},
			totalCount() {
				let count = 0;
				this.selectFoods.forEach((food)=>{
					count +=food.count
				});
				return count
			},
			payDesc() {
				if(this.totalPrice === 0){
					return `$${this.minPrice}元起送`
				}else if(this.totalPrice > 0  &&  this.totalPrice < this.minPrice){
					let priceTemp = this.minPrice - this.totalPrice;
					return `还差${priceTemp}元起送`
				}else{
					return "去结算"
				}
			}
		},
		components:{
			cartCtrl
		}
	}
</script>
<style scoped>
	
	.shopcart{
		display: flex;
		position: fixed;
		left:0;
		bottom:0;
		z-index: 2;
		width: 100%;
		height: 7%;
		background-color: #141d27;
		font-size: 18;
	}
	.shopcart .content-left{
		flex: 1;
		height: 100%;
		
	}
	.shopcart .content-left .logo-container{
		display: inline-block;
		position: absolute;
		left: 5%;
		top: -30%;
		width: 50px;
		height: 50px;
		border-radius: 50%;
		
		background-color: #000;
	}
	.shopcart .content-left .logo-wrapper{
		position: relative;
		left: 5px;
		top: 5px;
		width: 40px;
		height: 40px;
		border-radius: 50%;
		
		background-color: #fff;
		
	}
	.shopcart .content-left .logo-wrapper .count{
		position: absolute;
		
		height: 18px;
		border-radius: 30%;
		left: 46%;
		top: -26%;
		color: #fff;
		background-color: #FF0000;
		text-align: center;
		font-size: 14px;
		line-height: 14px;
		font-weight: 900;
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
		display: inline-block;

		position: absolute;
		left: 25%;
		width: 50px;
		height: 100%;
		color: rgba(255,255,255,0.4);
		font-size: 16px;
		line-height: 24px;
		font-weight: 700;
		line-height: 46px;
		border-right:1px solid #2b333b;
	}
	.shopcart .content-left .description{
		display: inline-block;

		position: absolute;
		left: 44%;
		height: 100%;
		color:rgba(255,255,255,0.4);
		font-size: 14px;
		font-weight: 500;
		line-height: 46px;
	}
	.shopcart .content-right{
		flex:0 0 100px;
		height: 100%;
		
	}
	.shopcart .content-right .pay{
		color: rgba(255,255,255,0.4);
		font-size: 12px;
		font-weight: 700;
		line-height: 46px;
		text-align: center;
		background-color: #2b333b;
	}
	.toGreen {
		background-color: #008000;
	}
	.shopcart .detail{
		position: fixed;
		width: 100%;
		height: 50%;
		bottom: 7%;
		z-index: -1;
		
		background-color: #fff;
	}
	.shopcart .detail .class-header{
		width: 100%;
		height: 40px;
		background-color: #f3f5f7;
	}
	.shopcart .detail .class-header .title{
		display: inline-block;
		width: 100px;
		height: 40px;
		margin-left:18px;
		color: rgb(7,17,27);
		font-size: 14px;
		line-height: 40px;
	}
	.shopcart .detail .class-header .empit{
		position: absolute;
		top: 0;
		right: 0;
		margin-right: 18px;
		font-size: 12px;
		line-height: 40px;
		color: rgb(0,160,220);
	}
	.shopcart .detail .list-content{
		
		overflow: hidden;
		height:100%;
		
	}
	
	.shopcart .detail .list-content .food{
		
		height: 48px;
		margin-left: 18px;
		list-style: none;
		border-bottom: 1px solid #ccc;
		
	}
	.shopcart .detail .list-content .food .name{
		display: inline-block;
		font-size: 14px;
		line-height: 48px;
		color: rgb(7,17,27);
	}
	.shopcart .detail .list-content .food .price{
		position: absolute;
		left: 52%;
		display: inline-block;
		font-size: 10px/14px;
		font-weight: 700;
		line-height: 48px;
		color: rgb(240,20,20);
	}
	.shopcart .detail .list-content .food .cartctrl{
		position: absolute;
		
		left: 68%;
		display: inline;
		margin-top: 6px;
	}
	
</style>

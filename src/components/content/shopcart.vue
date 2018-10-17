<template>
	<div class="shopcart">
			<div class="content-left">
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
			<div class="content-right">
				<div class="pay">
					{{payDesc}}
				</div>
			</div>
	</div>
</template>
<script>
	export default{
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
		background-color: #141d27;
		font-size: 0;
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
		font-size: 16px;
		font-weight: 700;
		line-height: 46px;
	}
	.shopcart .content-right{
		flex:0 0 100px;
		height: 100%;
		
	}
	.shopcart .content-right .pay{
		color: rgba(255,255,255,0.4);
		font-size: 13px;
		font-weight: 700;
		line-height: 46px;
		text-align: center;
		background-color: #2b333b;
	}
</style>

<template>
	<div class="goods">
		<slot></slot>
		<div class="container">
			<div class="menu-box" ref="mwrapper">
				<ul class="menu-wrapper" >
					<li class="menu" @click="selectMenu(index)" v-for="(item,index) in goods"  ref="menuhook" :class="{'curr':index==currIndex}">
						<span class="icon" v-show="item.type==-1">
							<img width="14" height="14" src="../../assets/images/discount_1@2x.png" alt="">
						</span>
						<span class="text">{{item.name}}</span>
					</li>
				</ul>
			</div>
			<div class="foods-wrapper" ref="fwrapper">
				<ul ref="s">
					<li  v-for="(item,Findex) in goods" class="food-list" ref="fhook">
						<h1 class="tittle">{{item.name}}</h1>
						<ul>
							<li class="food-item" v-for="(food,Sindex) in item.foods">
								<div class="icon">
									<img width="87" height="87" :src="food.icon" alt="">
								</div>
								<div class="content">
									<h2 class="name" @click="select(food)">{{food.name}}</h2>
									<p class="description">{{food.description}}</p>
								
									<div class="extra">
										<span class="count">月售{{food.sellCount}}份</span>
										<span>好评率{{food.rating}}%</span>
									</div>
									<div class="price">
										<span class="now">${{food.price}}</span>
										<span class="old" v-show="food.oldPrice">${{food.oldPrice}}</span>
									</div>
									<div class="cart-wrappear">
										<cartCtrl :food="food"></cartCtrl>
									</div>
									
								</div>
							</li>
						</ul>
					</li>
				</ul>
			</div>
		</div>
		<food :food="selectf" ref="food"></food>
		<shopcart :delivery-price="seller.deliveryPrice"
				  :min-price="seller.minPrice"
				  :select-foods="finalPrice"
				  :num="num"
					:selectFoods="selectFood">
		</shopcart>
	</div>
</template>
<script>
	import BScroll from 'better-scroll';
	import shopcart from './shopcart.vue';
	import cartCtrl from './cartCtrl.vue';
	import food from './food.vue';


	export default{
		data(){
			return {
				goods:[],
				seller:[],
				height:0,
				listHeight:[0],
				scrollY:0,
				finalPrice:[
					
				],
				num:0,
				selectf:{},
				
				index1:0,
				index2:0,
				is_show:false
			}
				
		},
		mounted(){
		},
		created(){
			this.$http({
				methods:'get',
				url:'api/goods'
			}).then(res => {
				this.goods = res.data.data;
				this.$nextTick(() => {
					this._initScroll();
					this.culScroll();
				});
			},res => {
				alert('err');
			}),
			this.$http({
				methods:'get',
				url:'api/seller'
				
			}).then(res => {
				
				this.seller = res.data.data;
				
				
			},res => {
				alert('err');
			})
		},
		methods:{
			select(food) {
				this.selectf = food;
				
				this.$refs.food.show();
			},
			_initScroll() {
				this.menuScroll = new BScroll(this.$refs.mwrapper,{
					probeType:3,click:true,taps:true
				});
				this.foodScroll = new BScroll(this.$refs.fwrapper,{
					probeType:3,click:true,taps:true
				});
				this.foodScroll.on('scroll',pos => {
					this.scrollY = Math.abs(Math.floor(pos.y));
				});
			},
			culScroll() {
				let foodList = this.$refs.fhook;
				let height = 0;
				for(let i = 0;i<foodList.length;i++){
					height += foodList[i].clientHeight;
					this.listHeight.push(height);
				}
			},
			selectMenu(index) {
				let temp = this.$refs.fhook[index];
				this.foodScroll.scrollToElement(temp,1000);
			}
		},
		computed:{
			currIndex() {
				for(let i = 0;i<this.listHeight.length;i ++){
					let height1 = this.listHeight[i];
					let height2 = this.listHeight[i+1];
					if ((this.scrollY>=height1&&this.scrollY<height2)||!height2){
						return i;
					}
				}
				return 0;
			},
			selectFood() {
				let foods = [];
				this.goods.forEach((good) => {
					good.foods.forEach((food) => {
						if(food.count>0){
							foods.push(food);
						}
					})
				});
				return foods;
			}
		},
		components:{
			shopcart,cartCtrl,food
		}
	}
</script>
<style scoped>
	.goods{
		position: fixed;
		top: 169px;
		width: 100%;
		height: 68%;
	}
	.container{
		display: flex;
		
		position: absolute;
		width: 100%;
		height: 100%;
		overflow: hidden;
	}
	.container .menu-box{
		width:80px;
		height: 100%;
		
	}
	.container .menu-wrapper{
		flex: 0 0 80px;
		
		flex-direction: column;
		
		
		background-color:  #f3f5f7;
		
		margin: 0;
		padding: 0;
	}
	.container .menu-wrapper .menu{
		flex: 1;
		flex-direction: column;
		list-style: none;
		display: table;
		width: 56px;
		height: 54px;
		line-height: 14px;
		padding: 0 12px;
		
	}
	.curr{
		background-color: #fff;
		z-index: 10;
	}
	.container .menu-wrapper .menu .icon{
		
		display: inline-block;
		margin-top: 10px;
		
	}
	.container .menu-wrapper .menu .text{
		display: table-cell;
		width: 56px;
		vertical-align: middle;
		font-size: 12px;
	}
	.container .foods-wrapper{
		flex: 1;
		
		
	}
	.container .foods-wrapper ul{
		list-style: none;
		padding: 0;
		margin: 0;
	}
	.container .foods-wrapper .tittle{
		padding-left: 14px;
		margin: 0;
		height: 26px;
		line-height: 26px;
		border-left: 2px solid #d9dde1;
		font-size: 12px;
		color: rgb(147,153,159);
		background: #f3f5f7;
	}
	.container .foods-wrapper .food-item{
		display: flex;
		margin: 18px;
		padding-bottom: 18px;
		flex-direction: row;
	}
	.container .foods-wrapper .food-item:last-child{
		padding-bottom: 0px;
	}
	.container .foods-wrapper .food-item .icon{
		flex: 0 0 57px;
		margin-right: 10px;
		
	}
	.container .foods-wrapper .food-item .content{
		display: flex;
		flex: 1;
		flex-direction: column;
	}
	.container .foods-wrapper .food-item .content .name{
		
		font-size: 17px;
		margin: 2px 0 8px 0;
		height: 14px;
		line-height: 14px;
		font-size: 14px;
		color: rgb(7,17,27);
	}
	.container .foods-wrapper .food-item .content .description{
		margin-bottom: 8px;
		line-height: 12px;
		font-size: 10px;
		color: rgb(147,153,159);
	
	}
	.container .foods-wrapper .food-item .content .extra{
		line-height: 10px;
		font-size: 10px;
		color: rgb(147,153,159);
	}
	.container .foods-wrapper .food-item .content .extra .count{
		margin-right: 12px;
	}
	.container .foods-wrapper .food-item .content .price{
		font-weight: 700;
		line-height: 24px;
	}
	.container .foods-wrapper .food-item .content .price .now{
		margin-right: 8px;
		font-size: 14px;color: rgb(240,20,20,);
	}
	.container .foods-wrapper .food-item .content .price .old{
		text-decoration: line-through;
		font-size: 10px;
		color: rgb(147,153,159);
	}
	.container .foods-wrapper .food-item .content .cart-wrappear{
		position: relative;
		right: -67px;
		bottom: 21px;
	}
	.container .foods-wrapper .food-item .content .cart-wrapper{
		width: 100px;
		height: 30px;
		background-color: #000000;
		position: relative;
		left: 50%;
		top: 10%;
	}
	
	


</style>

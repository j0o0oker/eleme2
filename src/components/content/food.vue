<template>
	<div class="container" ref="f" v-show="myshow">
			<div class="food">
				<div class="close" @click="close">关闭</div>
				<div class="img">
					<img  :src="food.image" alt="">
				</div>
				<div class="description">
					<div class="des-left">
						<div class="name">{{food.name}}</div>
						<div class="des">
							<div class="count">月售{{food.sellCount}}份</div>
							<div class="rating">好评率{{food.rating}}%</div>
						</div>
						<div class="price">
							<div class="nowPrice">${{food.price}}</div>
							<div class="oldPrice">{{food.oldPrice}}</div>
						</div>
					</div>
					<div class="des-right">
						<div class="join" v-show="food.count==0">加入购物车</div>
						<div class="cartCtrl">
							<cartCtrl :food="food" v-show="food.count>0"></cartCtrl>

						</div>
					</div>
				</div>
				<div class="line">
					<grayLine></grayLine>
				</div>
				<div class="food-des">
					<div class="title">商品介绍</div>
					<div class="centont">{{food.info}}</div>
				</div>
				<div class="line">
					<grayLine></grayLine>
				</div>
				<div class="rating-select">
					<ratingsSelect @change="changer" :ratings="food.ratings"></ratingsSelect>
				</div>
				<div class="appraise-wrapper">
					<ul>
						<li class="appraise-list" v-for="(item,index) in food.ratings" v-show="ishow(index,rateType)">
							<div class="user-info">
								<div class="time">{{item.rateTime}}</div>
								<div class="name">{{item.username}}</div>
								<div class="avatar">
									<img width="20" height="20" :src="item.avatar" alt="">
								</div>
							</div>
							<div class="info">{{item.text}}</div>
						</li>
					</ul>
				</div>
			</div>
	</div>
</template>
<script>
	import BScroll from 'better-scroll';
	import cartCtrl from './cartCtrl.vue';
	import ratingsSelect from './ratingsSelect.vue';
	import grayLine from '../grayLine.vue';


	export default{
		data(){
			return {
				myshow:false,
				rateType:-1,
				checked:false
			}
		},
		props:{
		
			food:{
				type:Object,
				default:function() {
					{}
				}
			}
		},
		
		updated() {
			this.$nextTick(() => {
				this._detailScroll();
				
			});
		},
		methods: {
			changer(val) {
				console.log(val)
				this.checked = val.checked;
				this.rateType = val.rateType;
			},
			ishow(index,rateType) {
				if(this.checked === true){
					if(rateType === -1 && this.food.ratings[index].text !== ""){
						return true;
					}else if(this.food.ratings[index].rateType === rateType && this.food.ratings[index].text !== ""){
						return true;
					}
				}else {
					if(rateType === -1){
						return true;
					}else if(this.food.ratings[index].rateType === rateType){
						return true;
					}
				}
			},
			_detailScroll() {
				this.detailScroll = new BScroll(this.$refs.f,{
					probeType:3,click:true,taps:true
				});
			},
			show() {
				this.myshow = true;
			},
			close() {
				this.myshow = false;
			}
		},
		components:{
			cartCtrl,ratingsSelect,grayLine
		}
	}
</script>
<style scoped>
	.container{
		position: fixed;
		width: 100%;
		height: 97%;
		left: 0;
		top: 0;
		background-color: #fff;
		bottom: 47px;
		overflow: hidden;
	}
	.container .food{
		height: 10000px;
	}
	.container .food .img img{
		position: relative;
		width: 100%;
		
	}
	.container .food{
		position: relative;
	}
	.container .food .close{
		text-align: center;
		background-color: rgba(0,0,0,0.4);
	}
	.container .food .description{
		display: flex;
		margin: 18px;
	}
	.container .food .description .des-left{
		flex:1;
	}
	.container .food .description .des-left .name{
		font-size: 20px;
		font-weight: 700;
	}
	.container .food .description .des-left .des{
		display: flex;
		margin-top: 8px;
		font-size: 16px;
		font-weight: 500;
		color: #ccc;
	}
	.container .food .description .des-left .price{
		margin-top: 18px;
		font-size: 20px;
		font-weight: 700;
		color: red;
	}
	.container .food .description .des-right{
		flex:0 0 100px;
	}
	.container .food .description .des-right .join{
		position: relative;
		top: 65px;
		left: -61px;
		width: 100px;
		height: 34px;
		background-color: #2A7DCF;
		border-radius: 34px;
		line-height: 34px;
		font-size: 17px;
		text-align: center;
		color: #f3f5f7;
	}
	.container .food .description .des-right .cartCtrl{
		position: relative;
		top: 37px;
		right: 49px;
	}
	.container .food .food-des{
		position: relative;
		margin:18px 0 18px 0;	
	}
	 .container .appraise-wrapper .appraise-list{
		list-style: none;
		border-bottom: 1px solid #ccc;
		
	}
	 .container .appraise-wrapper .appraise-list .user-info{
		display: flex;
		margin-top: 18px;
		color: #ccc;
		margin-bottom: 18px;
	}
	 .container .appraise-wrapper .appraise-list .user-info .name{
		position: relative;
		right: -38%;
	}
	 .container .appraise-wrapper .appraise-list .user-info .avatar{
		width: 20px;
		height: 20px;
		border-radius: 50%;
		overflow: hidden;
		position: relative;
		right: -38%;
	}
	.container .appraise-wrapper .appraise-list .info{
		font-size: 18px;
		height: 60px;
		
	}
	
	
</style>

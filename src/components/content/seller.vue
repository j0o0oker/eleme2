<template>
	<div class="seller">
		<slot></slot>
		<div class="content">
			<div class="seller-info">
				<span class="title">{{seller.name}}</span>
				<div class="star">
					<star :score="seller.score"></star>
				</div>
				<div class="count">月售{{seller.sellCount}}单</div>
			</div>
			<div class="collect">
				<i class="iconfont icon-shoucang1" :class="{toRed:is_show}" @click="is_show=!is_show"></i>
				<span class="text" v-show="is_show">已收藏</span>
			</div>
			<div class="grayLine">
				<grayLine></grayLine>
			</div>
			<div class="price-info">
				<div class="minPrice">
					<span class="text">起送价</span>
					<span class="number">{{seller.minPrice}}元</span>
				</div>
				<div class="deliveryPrice">
					<span class="text">商家配送</span>
					<span class="number">{{seller.deliveryPrice}}元</span>
				</div>
				<div class="deliveryTime">
					<span class="text">平均配送时间</span>
					<span class="number">{{seller.deliveryTime}}分钟</span>
				</div>
			</div>
			<div class="grayLine">
				<grayLine></grayLine>
			</div>
			<div class="announcement">
				<span title>公告与活动</span>
				<p>{{seller.bulletin}}</p>
			</div>
		</div>
	</div>
</template>
<script>
	import grayLine from '../grayLine.vue';

	import star from '../star.vue';
	export default{
		data(){
			return {
				seller:[],
				is_show:false
			}
		},
		created(){
			this.$http({
				methods:'get',
				url:'api/seller'
			}).then((res) => {
				this.seller = res.data.data;
				console.log(this.seller);
			},(res) => {
				
			})
		},
		computed:{},
		components:{
			star,grayLine
		}
	}
</script>
<style scoped>
	.content{
		position: fixed;
		top: 32%;
		width: 100%;
		height: 68%;
		overflow: hidden;
	}
	.content .seller-info {
		display: inline-block;
		margin: 18px 0 18px 18px;
	}
	.content .seller-info .title {
		display: block;
		margin-bottom: 8px;
		font-size: 14px;
		color: rgb(7,17,27);
		line-height: 14px;
	}
	.content .seller-info .star {
		display: inline-block;
		margin-right: 16px;
		margin-bottom: 18px;
	}
	.content .seller-info .count {
		display: inline-block;
	}
	.content .price-info {
		margin-top: 18px;
		margin-bottom: 36px;
		text-align: center;
	}
	.content .price-info .minPrice {
		display: inline-block;
		margin-left: 0px;
	}
	.content .price-info .minPrice .text{
		display: block;
		font-size: 10px;
		line-height: 10px;
		color: rgb(147,153,159);
		
	}
	.content .price-info .minPrice .number{
		display: block;
		margin-top: 4px;
		font-size: 24px/20px;
		font-weight: 200;
		line-height: 24px;
		color: rgb(7,17,27);
	}
	.content .price-info .deliveryPrice {
		display: inline-block;
		margin-left: 57px;

		
	}
	.content .price-info .deliveryPrice .text{
		display: block;
		font-size: 10px;
		line-height: 10px;
		color: rgb(147,153,159);
	}
	.content .price-info .deliveryPrice .number{
		display: block;
		margin-top: 4px;

		font-size: 24px/20px;
		font-weight: 200;
		line-height: 24px;
		color: rgb(7,17,27);
	}
	.content .price-info .deliveryTime {
		display: inline-block;
		margin-left: 53px;

	}
	.content .price-info .deliveryTime .text{
		display: block;
		font-size: 10px;
		line-height: 10px;
		color: rgb(147,153,159);
	}
	.content .price-info .deliveryTime .number{
		display: block;
		margin-top: 4px;

		font-size: 24px/20px;
		font-weight: 200;
		line-height: 24px;
		color: rgb(7,17,27);
	}
	.content .collect {
		position: absolute;
		top: 20px;
		right: 18px;
		display: inline-block;
	}
	.content .collect i {
		display: block;
		text-align: center;
	}
	.toRed {
		color: red;
	}
	.content .collect .text{
		display: block;
	}
	.content .announcement {
		margin-top: 36px;
		margin-left: 18px;
	}
	.content .announcement .title {
		display: block;
		margin-bottom: 8px;
		font-size: 14px;
		color: rgb(7,17,27);
		line-height: 14px;
	} 
	.content .announcement p {
		display: block;
		margin-top: 8px;
		font-size: 12px;
		font-weight: 200;
		color: rgb(240,20,20);
		line-height: 24px;
	} 
</style>

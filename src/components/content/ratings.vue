<template>
	<div class="content" ref="ratinghock">
	
		<slot></slot>
		<div>
			<div class="rating-detail">
				<div class="remark">
					<span class="score">{{culScore}}</span>
					<span class="text">综合评分</span>
					<span class="rate">高于周边商家66.6%</span>
				</div>
				<div class="altitude">
					<span class="text">服务态度</span>
					<div class="star">
						<star :score="culScore"></star>
					</div>
					<span class="arrivetime">送达时间</span>
					<span class="time">44分钟</span>
				</div>
			</div>
			<div class="gray-line">
				<grayLine></grayLine>
			</div>
			<div class="rating-select">
				<ratingsSelect @change="changer" :ratings="ratings"></ratingsSelect>
			</div>
			<div class="appraise-wrapper">
				<ul>
					<li class="appraise-list" v-for="(item,index) in ratings" v-show="ishow(index,rateType)">
						<div class="avatar">
							<img width="28" height="28" :src="item.avatar" alt="">
						</div>
						<div class="user-info">
							<span class="name">{{item.username}}</span>
							<div class="star">
								<star :score="item.score"></star>
							</div>
							<div class="deliveryTime" v-show="item.deliveryTime!==''">{{item.deliveryTime}}分钟送达</div>
						</div>
						<div class="time">{{item.rateTime}}</div>
						<div class="text">{{item.text}}</div>
						<div class="recommends">
							<ul>
								<li class="recommend" v-for="recommend in item.recommend">{{recommend}}</li>
							</ul>
						</div>
					</li>
				</ul>
			</div>
		</div>
	</div>
</template>
<script>
	import BScroll from 'better-scroll';
	import star from '../star.vue';
	import grayLine from '../grayLine.vue';
	import ratingsSelect from './ratingsSelect.vue';
	
	export default{
		data(){
			return {
				ratings:[],
				rateType:-1,
				checked:false
			}
		},
		updated() {
			this._ratingScroll();
		},
		created(){
			this.$http({
				methods:'get',
				url:'api/ratings'
			}).then((res) =>{
				this.ratings = res.data.data;
				
			},(res) => {
				
			})
		},
		methods:{
			changer(val) {
				console.log(val)
				this.checked = val.checked;
				this.rateType = val.rateType;
			},
			ishow(index,rateType) {
				if(this.checked === true){
					if(rateType === -1 && this.ratings[index].text !== ""){
						return true;
					}else if(this.ratings[index].rateType === rateType && this.ratings[index].text !== ""){
						return true;
					}
				}else {
					if(rateType === -1){
						return true;
					}else if(this.ratings[index].rateType === rateType){
						return true;
					}
				}
			},
			_ratingScroll() {
				let scroll = new BScroll(this.$refs.ratinghock,{
					probeType:3,click:true,taps:true
				});
				
			}
		},
		computed:{
			culScore() {
				let score = 0;
				this.ratings.forEach((rating) => {
					score += rating.score
				});
				score = Math.floor(score/this.ratings.length*10)/10;
				return score;
			},
			culTime() {
				let times = 0;
				this.ratings.forEach((time) => {
					times += time.deliveryTime
				});
				times = times/this.ratings.length;
				 return times;
			}
		},
		components:{
			star,grayLine,ratingsSelect
		}
	}
</script>
<style scoped>
	ul,li{
		list-style: none;
		margin: 0;
		padding: 0;
	}
	.content {
		position: fixed;
		top: 32%;
		width: 100%;
		height: 68%;
		overflow: hidden;
	}
	.content .rating-detail {
		
	}
	.content .rating-detail .remark {
		display: inline-block;
		width: 40%;
		height: 99px;
		
	}
	.content .rating-detail .remark .score {
		display: block;
		width: 100%;
		height: 24px;
		margin-top: 18px;
		line-height: 24px;
		font-size: 24px;
		font-weight: 900;
		text-align: center;
		color: gold;
	}
	.content .rating-detail .remark .text {
		display: block;
		width: 100%;
		height: 12px;
		margin-top: 6px;
		line-height: 12px;
		font-size: 12px;
		font-weight: 600;
		text-align: center;
		color: #000;
	}
	.content .rating-detail .remark .rate {
		display: block;
		width: 100%;
		height: 10px;
		margin-top: 5px;
		line-height: 10px;
		font-size: 10px;
		font-weight: 600;
		text-align: center;
		color: #ccc;
	}
	.content .rating-detail .altitude {
		position: absolute;
		display: inline-block;
		width: 58%;
		height: 99px;
	}
	.content .rating-detail .altitude .text {
		display: inline-block;
		margin-top: 18px;
		margin-right: 12px;
		font-size: 12px;
	}
	.content .rating-detail .altitude .star {
		
		display: inline-block;
		width: 132px;
	}
	.content .rating-detail .altitude .arrivetime {
		
		display: inline-block;
		margin-bottom: 25px;
		font-size: 12px;
	}
	.content .rating-detail .altitude .time {
		
		display: inline-block;
		margin-bottom: 25px;
		margin-left: 12px;
		font-size: 12px;
		color: #ccc;
	}
	.content .appraise-wrapper{
		border-top: 1px solid #ccc;
		margin: 0;
		padding: 0;
	}
	.content .appraise-wrapper .appraise-list{
		list-style: none;
		border-bottom: 1px solid #ccc;
	}
	.content .appraise-wrapper .appraise-list .avatar {
		display: inline-block;
		width: 28px;
		height: 28px;
		margin: 18px 12px 6px 18px;
		border-radius: 50%;
		overflow: hidden;
	}
	.content .appraise-wrapper .appraise-list .user-info {
		display: inline-block;
	}
	.content .appraise-wrapper .appraise-list .user-info .name {
		display: block;
		font-size: 10px;
		color: rgb(7,17,27);
	}
	.content .appraise-wrapper .appraise-list .user-info .star {
		display: inline;
		font-size: 10px;
		color: rgb(7,17,27);
	}
	.content .appraise-wrapper .appraise-list .user-info .deliveryTime {
		display: inline;
		font-size: 10px;
		font: 200;
		color: rgb(147,153,159);
		line-height: 12px;
	}
	.content .appraise-wrapper .appraise-list .time {
		position: absolute;
		right: 0;
		display: inline-block;
		margin-top: 18px;
		font-size: 10px;
		font-weight: 200;
		line-height: 24px;
		color: rgb(147,153,159);
	}
	.content .appraise-wrapper .appraise-list .text {
		margin-left: 46px;
		margin-bottom: 8px;
		font-size: 12px;
		font-weight: 200;
		line-height: 24px;
		color: rgb(7,17,27);
	}
	.content .appraise-wrapper .appraise-list .recommends {
		display: inline-block;
		margin-left: 47px;
	}
	.content .appraise-wrapper .appraise-list .recommend {
		float: left;
		margin-right: 5px;
		font-size: 9px;
		color: rgb(147,153,159);

	}
</style>


<!-- 加在父组件上 -->
<!-- <ratingsSelect @change="changer"></ratingsSelect> -->
<!-- 	changer(val) {
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
			} -->

<template>
	<div class="ratingSelect">
		<div class="title">商品评价</div>
		<div class="nav">
			<div class="all" @click.stop="all">全部{{ratings.length}}</div>
			<div class="good" @click.stop="good">推荐{{culGoodNum}}</div>
			<div class="bad" @click.stop="bad">吐槽{{culBadNum}}</div>
		</div> 
		<div class="allContent">
			<div class="filter">
				<input type="checkbox" @click="select($event)">只看有内容的评价
			</div>
			
		</div>
	</div>
</template>
<script>
	export default {
		data() {
			return {
				
				checked:false
			}
		},
		props: {
			ratings: {
				type: Array,
				default() {
					return {}
				}
			}
		},
		methods: {
			select(e) {
				
				this.checked = e.target.checked;
				console.log(this.checked);
			},
			all() {
				// console.log(111);
				this.$emit("change",{rateType:-1,checked:this.checked});
				
			},
			good() {
				// console.log(222);
				this.$emit("change",{rateType:0,checked:this.checked});
				
			},
			bad() {
				// console.log(333);
				this.$emit("change",{rateType:1,checked:this.checked});
				
			}
		},
		computed: {
			culGoodNum() {
				let arr = [];
				for(let i = 0;i<this.ratings.length;i++){
					if(this.ratings[i].rateType === 0){
						arr.push(this.ratings[i]);
					};
				};
				return arr.length;
			},
			culBadNum() {
				let arr = [];
				for(let i = 0;i<this.ratings.length;i++){
					if(this.ratings[i].rateType === 1){
						arr.push(this.ratings[i]);
					};
				};
				return arr.length;
			}
		}
	}
</script>
<style scoped>
	.title{
		margin-top: 18px;
		margin-left: 18px;

		font-size: 18px;
		font-weight: 700;
	}
	.nav{
		display: flex;
		width: 400px;
		margin:18px 0 18px 18px;
		border-bottom: 1px solid #ccc;
		font-size: 18px;
	}
	.nav .all{
		width: 80px;
		height: 34px;
		background-color: rgba(0,160,220);
		color: #fff;
		line-height: 34px;
		text-align: center;
		border-radius: 2px;
		margin-bottom: 18px;
		
		
	}
	.nav .good{
		width: 80px;
		height: 34px;
		margin-left: 8px;
		background-color: rgb(0,160,220,.2);
		color: rgb(77,85,93);
		line-height: 34px;
		text-align: center;
		border-radius: 2px;
		margin-bottom: 18px;
	}
	.nav .bad{
		width: 80px;
		height: 34px;
		margin-left: 8px;
		background-color: rgba(75,85,93,.2);
		color:  rgb(77,85,93);
		line-height: 34px;
		text-align: center;
		border-radius: 2px;
		margin-bottom: 18px;
	}
	.allContent .filter{
		font-size: 12px;
		color: #ccc;
		margin-top: 12px;
		margin-bottom: 12px;
		
	}
	
</style>

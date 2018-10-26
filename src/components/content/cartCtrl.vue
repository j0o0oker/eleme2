<template>
		<div class="cartctrl">
			<div class="cart-decrease" v-show="food.count>0" @click.stop.prevrnt="decrease">
				<i class="iconfont icon-jianshao"></i>

			</div>
			<div class="cart-count" v-show="food.count>0">{{food.count}}</div>
			<div class="cart-add" @click.stop.prevrnt="add">
				<i class="iconfont icon-htmal5icon18"></i>
			</div>
		</div>
	
</template>
<script>
	import Vue from 'vue';
	export default{
		props:{
			food:{
				type:Object
			}
		},
		created() {
			
			
		},
		data(){
			return {
				num:0
			}
		},
		methods:{
			add() {
				if(!this.food.count){
					Vue.set(this.food,'count',1);
				}else{
					this.food.count++;
					console.log(this.food.count);
				}
			},
			decrease() {
				this.food.count--;
			}
		},
		computed:{
			
		},
		components:{}
	}
</script>
<style scoped>
	.cartctrl {
		height: 24px;
		width: 103px;
	}
	i {
		
		font-size: 22px;
		text-align: center;
		line-height: 24px;
		color: rgb(1,100,225);


	}
	.cartctrl .cart-decrease {
		display: inline-block;
		vertical-align: middle;
		
	}
	.cartctrl .cart-count{
		display: inline-block;
		width: 49px;
		font-size: 10px;
		color: rgb(147,153,159);
		text-align: center;
		line-height: 24px;

	}
	.cartctrl .cart-add {
		
		display: inline-block;
		vertical-align: middle;

	}
	
</style>

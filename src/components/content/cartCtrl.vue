<template>
	
		<div class="select">
			<div class="reduce" @click="reduce">
				<div class="reduceIcon">-</div>
				<div class="text">{{num}}</div>
			</div>
			<div class="add" @click="add">+</div>
		</div>
	
</template>
<script>
	export default{
		data(){
			return {
				num:0
			}
		},
		created(){
			
		},
		methods:{
			add() {
				this.num +=1;
				this.$emit("want",this.num);
			},
			reduce() {
				this.num -=1;
				this.$emit("want",this.num);
			}
		},
		computed:{
			
		},
		components:{}
	}
</script>
<style scoped>
	.select{
		display: flex;
		position: relative;
		top: -23px;
		left:40%;
		background-color: ;
		width: 60%;
		height: 25px;
	}
	.select .reduce{
		flex:1;
		
	}
	.select .reduce .reduceIcon{
		width: 30px;
		height: 30px;
		border-radius: 50%;
		background-color: #FF6A6A;
		color: #fff;
		font-size: 28px;
		line-height: 23px;
		text-align: center;
	}
	.select .reduce .text{
		position: relative;
		top: -107%;
		left:24%;
		text-align: center;
	}
	.select .add{
		flex: 0 0 30px;
		width: 30px;
		height: 30px;
		border-radius: 50%;
		color: #fff;
		font-size: 28px;
		line-height: 23px;
		text-align: center;
		background-color: #2a7dcf;
		
	}
</style>

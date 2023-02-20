<template>
	<view>
		<view class="place4"><text>请选择要换算的币种后输入数额</text></view>
		<view class="place4 row"><text>换算金额</text><input @blur="type" :value="this.num"/></view>
		<view class="place4 row"><text>原始货币</text>
		<picker mode="selector" :range="money" @change="inserti">
			<view class="place9">
			{{money[this.i]}}
			</view>
	</picker>
	</view>
		<view class="place4 row"><text>目标货币</text>
	<picker mode="selector" :range="money" @change="insertj">
			<view class="place9">
			{{money[this.j]}}
			</view>
	</picker>	
		
		</view>
		<view class="place4">
			<button v-on:click="com" type="primary">计算</button>
			<textarea :value="res"/>
		</view>
	</view>
</template>

<script>
	let res
	export default {
		data() {
			return {
				money:['美元(USD)','人民币(CNY)','加元(CAD)','港币(HKD)','英镑(GBP)','欧元(EUR)','日元(JPY)'],
				num:1,
				i:0,
				j:0,
				res:''
				}
		},
		methods: {
				
			com(){
				this.res=this.num+this.money[this.i]+"="+this.num*rate[i]+this.money[this.j]
			},
			type(e){
				this.num=e.detail.value
			},
			inserti(e){
				this.i=e.detail.value
			},
			insertj(e){
				this.j=e.detail.value
			},
		}
	}
</script>

<style>

</style>

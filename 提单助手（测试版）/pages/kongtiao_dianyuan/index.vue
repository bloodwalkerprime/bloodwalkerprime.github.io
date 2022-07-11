<template>
	<view style="display: flex;margin-top: 10rpx;">
		<text class="css_kongtiao_dianyuan_text">开关电源{{kongtiao_dianyuan_number}}---</text>
		<text class="css_kongtiao_dianyuan_text">负载：</text>
		<input class="kongtiao_fianyuan_input" v-model="kongtiao_dianyuan_fz"  @blur="shiqu"/>
		<text class="css_kongtiao_dianyuan_text">V</text>
	</view>
</template>

<script>
	export default {
		props:{numberkt:Number},
		data() {
			return {
				kongtiao_dianyuan_number:this.numberkt,
				kongtiao_dianyuan_fz:"",
				kongtiao_dianyuan_end:"",
				}
			},
		methods:{
			shiqu(){
				console.log("负载失去聚焦");
				this.kongtiao_dianyuan_end="开关电源"+this.kongtiao_dianyuan_number
				+"，负载："+this.kongtiao_dianyuan_fz+"V，";
				this.$emit('dianyuan_fz',this.kongtiao_dianyuan_end);
			}
		}
		}
</script>

<style>
	.kongtiao_fianyuan_input{
		border:#000 1rpx solid;
		width: 200rpx;
	}
	.css_kongtiao_dianyuan_text{
		margin-left: 10rpx;
	}
</style>
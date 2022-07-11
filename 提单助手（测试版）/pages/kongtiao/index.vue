<template>
	<view style="border:#000 1rpx solid;margin-left: 10rpx;margin-right: 10rpx;">
		<dianyuan v-for="index in kongtiao_dianyuan_for" @dianyuan_fz="dianyuan_fz" :numberkt="numberkt"></dianyuan>
		<view style="display:flex;">
			<button @click="kongtiao_dianyuan_sub">电源-</button>
			<button @click="kongtiao_dianyuan_add">电源+</button>
		</view>
		<kongtiao  v-for="index in kongtiao_for" @kongtiao_callback="kongtiao_callback" :numberkkt="numberkkt"></kongtiao>
		<view style="display:flex;">
			<button @click="kongtiao_sub">空调-</button>
			<button @click="kongtiao_add">空调+</button>
		</view>
		<button @click="kongtiao_finally">编写完成请点击</button>
	</view>
</template>

<script>
	import dianyuan from '../kongtiao_dianyuan/index.vue'
	import kongtiao from '../kongtiao_num/index.vue'
	export default {
		components: {
			dianyuan,kongtiao
		},
		data() {
			return {
				kongtiao_dianyuan_for:[{}],
				kongtiao_for:[{}],
				numberkt:1,
				numberkkt:1,
				kongtiao_end:"",
				}
			},
		methods:{
			dianyuan_fz(e){
				this.kongtiao_end=this.kongtiao_end.concat(e)
			},
			kongtiao_callback(e){
				this.kongtiao_end=this.kongtiao_end.concat(e)
				console.log(this.kongtiao_end)
			},
			kongtiao_dianyuan_add(){
				this.numberkt+=1;
				this.kongtiao_dianyuan_for.push({});
			},
			kongtiao_dianyuan_sub(){
				this.numberkt-=1;
				this.kongtiao_dianyuan_for.pop({})
			},
			kongtiao_add(){
				this.numberkkt+=1;
				this.kongtiao_for.push({});
			},
			kongtiao_sub(){
				this.numberkkt-=1;
				this.kongtiao_for.pop({});
			},
			kongtiao_finally(){
				this.$emit('kongtiao_end',this.kongtiao_end)
			}
		}
		}
</script>

<style>
</style>
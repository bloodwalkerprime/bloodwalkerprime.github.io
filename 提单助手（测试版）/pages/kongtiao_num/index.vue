<template>
	<view style="margin-left: 10rpx;">
		空调{{kongtiao_number}}
		<view style="display: flex;margin-top: 10rpx;">
			<text>品牌型号：</text>
			<input class="kongtiao_input" type="text" v-model="kongtiao_pp">
		</view>
		<view style="display: flex;margin-top: 10rpx;">
			<text>生产日期：</text>
			<input class="kongtiao_input" type="text" v-model="kongtiao_scrq">
			<text>年</text>
		</view>
		<radio-group>
			<radio @click="kongtiao_hao();kongtiao_end_functions();">正常可用</radio>
			<radio @click="kongtiao_huai">不可用</radio>
		</radio-group>
		<view v-if="ktgz">
			故障类型：
				<radio-group @click="kongtiao_end_functions">
					<radio @click="ysjgz">压缩机故障</radio>
					<radio @click="lfly">漏氟漏液</radio>
					<radio @click="sblh">设备老化</radio>
					<radio @click="bgz">不工作</radio>
					<radio @click="bd">被盗</radio>
				</radio-group>
		</view>
	</view>
</template>

<script>
	export default {
		props:{numberkkt:Number},
		data() {
			return{
				kongtiao_number:this.numberkkt,
				kongtiao_scrq:"",
				kongtiao_pp:"",
				haoorhuai:"",
				kongtiao_end:"",
				ktgz:false,
				gzlx:"",
			}
		},
		methods:{
			kongtiao_end_functions(){
				if(this.haoorhuai==="正常可用"){
					this.kongtiao_end="空调"+this.kongtiao_number+",品牌："+this.kongtiao_pp
					+"，生产日期："+this.kongtiao_scrq+"年,"+this.haoorhuai+"。"
				}else if(this.haoorhuai==="不可用"){
					this.kongtiao_end="空调"+this.kongtiao_number+",品牌："+this.kongtiao_pp
					+"，生产日期："+this.kongtiao_scrq+"年,"+this.haoorhuai+"。"
					+"因空调"+this.gzlx+"，无法满足散热需求，申请空调整治"
				}else{
					this.kongtiao_end="111"
				}
				this.$emit('kongtiao_callback',this.kongtiao_end);
			},
			kongtiao_hao(){
				this.haoorhuai="正常可用";
				this.ktgz=false;

			},
			kongtiao_huai(){
				this.haoorhuai="不可用";
				this.ktgz=true;
			},
			ysjgz(){this.gzlx="压缩机故障";},
			lfly(){this.gzlx="漏氟漏液";},
			sblh(){this.gzlx="设备老化";},
			bgz(){this.gzlx="不工作";},
			bd(){this.gzlx="被盗";}
		},
	}
</script>

<style>
	.kongtiao_input{
		border:1rpx #000 solid;
		width: 300rpx;
	}
</style>
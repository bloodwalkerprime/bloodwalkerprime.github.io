<template>
	<view class="css_dainchi_all">
		<view class="css_dainchi_view">
			<text>开关电源{{number_dianchi}}:</text>
			<radio-group >
				<radio @click="G4">4G</radio>
				<radio @click="G5">5G</radio>
				<radio @click="G_45">4+5G</radio>
			</radio-group>
		</view>
		<view class="css_dainchi_view"> 
			<text>品牌型号：</text>
			<input class="css_dianchi_input" type="text" v-model="kgdy.ppxh_kgdy" placeholder="安耐特"></input>
		</view>
		<view class="css_dainchi_view">
			<text>下挂业务：</text>
			<input class="css_dianchi_input" type="text" v-model="kgdy.yw" placeholder="移动4G+电信4G+联通4G"></input>
		</view>
		<view class="css_dainchi_view">
			<text>总体负载：</text>
			<input class="css_dianchi_input" type="text" v-model="kgdy.fz" placeholder="55.3"></input>
			<text>V</text>
		</view>
		<view class="css_dainchi_view" v-show="is_45">
			<text>5G 负 载：</text>
			<input class="css_dianchi_input" type="text" v-model="kgdy.fz_5" placeholder="55.3"></input>
			<text>V</text>
		</view>
		<view class="css_dainchi_view">
			<text>生产日期：</text>
			<input class="css_dianchi_input" type="text" v-model="kgdy.scrq_kgdy" placeholder="2022"></input>
			<text>年</text>
		</view>
		<view class="css_dainchi_view">
			<text>下挂模块：</text>
			<input class="css_dianchi_input" type="text" v-model="kgdy.mks" placeholder="2"></input>
			<text>个</text>
		</view>
		<view class="css_dainchi_view">
			<radio-group >
				<radio @click="youbeidian">有备电</radio>
				<radio @click="wubeidian">无备电</radio>
			</radio-group>
		</view>
		<view v-show="kgdy.v_if_beidian">
			<view class="css_dainchi_view">
				<button :class="css_button_1" @click="click_button_tieli">铁锂</button>
				<button :class="css_button_2" @click="click_button_qiansuan">铅酸</button>
				<button :class="css_button_3" @click="click_button_tici">梯次</button>
			</view>
			<view class="css_dainchi_view">
				<text>电池品牌：</text>
				<input class="css_dianchi_input" type="text" v-model="kgdy.ppxh_dc" placeholder="双登"></input>
			</view>
			
			<view class="css_dainchi_view">
				<text>生产日期：</text>
				<input class="css_dianchi_input" type="text" v-model="kgdy.scrq_dc" placeholder="2022"></input>
				<text>年</text>
			</view>
			<view class="css_dainchi_view">
				<text>电池数量：</text>
				<input class="css_dianchi_input" type="text" v-model="kgdy.sl_dc" placeholder="2"></input>
				<text>组</text>
			</view>
			<view class="css_dainchi_view">
				<text>电池容量：</text>
				<input class="css_dianchi_input" type="text" v-model="kgdy.dcrl_dc" placeholder="25"></input>
				<text>Ah</text>
			</view>
			<view class="css_dainchi_view">
				<text>备电时长：</text>
				<input class="css_dianchi_input" type="text" v-model="kgdy.bdsc_dc" placeholder="60"></input>
				<text>分钟</text>
			</view>
		</view>
		<button :class="title_error" @click="callback">{{title_button_end}}</button>
	</view>
</template>

<script>
export default {
	props:{number:Number},
	data() {
		return {
			number_dianchi:this.number,
			beidian:null,//单选按钮的值
			css_button_1:"css_button_up",
			css_button_2:"css_button_up",
			css_button_3:"css_button_up",
			title_error:"title_success",
			title_button_end:"填写完请点击",
			is_45:false,
			kgdy:{
					g_45:"",
					fz:"",
					fz_5:"",
					dczl:"",
					ppxh_kgdy:"",
					scrq_kgdy:"",
					yw:"",
					mks:"",
					v_if_beidian:"",
					ppxh_dc:"",
					scrq_dc:"",
					dcrl_dc:"",
					sl_dc:"",
					bdsc_dc:"",
					xqxq:"",
				},
			dc_end:"",
		}
	},
	methods:{
		youbeidian(){
			this.kgdy.beidian="有备电";
			console.log(this.kgdy.beidian);
			if(this.kgdy.beidian==="有备电"){
				this.kgdy.v_if_beidian=true;
			}
		},
		wubeidian(){
			this.kgdy.beidian="无备电";
			console.log(this.kgdy.beidian);
			if(this.kgdy.beidian==="无备电"){
				this.kgdy.v_if_beidian=false;
			}
		},
		G4(){
			this.kgdy.g_45="4";
			this.is_45=false;
		},
		G5(){
			this.kgdy.g_45="5";
			this.is_45=false;
		},
		G_45(){
			this.kgdy.g_45="4+5";
			this.is_45=true;
		},
		click_button_tieli(){
			this.kgdy.dczl="铁锂";
			this.css_button_1="css_button_down";
			this.css_button_2="css_button_up";
			this.css_button_3="css_button_up";
		},
		click_button_qiansuan(){
			this.kgdy.dczl="铅酸";
			this.css_button_1="css_button_up";
			this.css_button_2="css_button_down";
			this.css_button_3="css_button_up";
		},
		click_button_tici(){
			this.kgdy.dczl="梯次";
			this.css_button_1="css_button_up";
			this.css_button_2="css_button_up";
			this.css_button_3="css_button_down";
		},
		callback(){
			if(this.kgdy.beidian==="有备电"){
				if(this.kgdy.g_45=="4+5"){
					this.dc_end=this.kgdy.g_45+"G开关电源"+this.number_dianchi+"（业务："+this.kgdy.yw+"),总负载:"
					+this.kgdy.fz +"V，5G负载："+this.kgdy.fz_5 +"V，品牌："+this.kgdy.ppxh_kgdy+"、生产日期："
					+this.kgdy.scrq_kgdy+"年、模块数："+this.kgdy.mks+"个,下挂"+this.kgdy.sl_dc
					+"组"+this.kgdy.scrq_dc+"年"+this.kgdy.ppxh_dc+this.kgdy.dcrl_dc+"Ah"+this.kgdy.dczl
					+"电池。备电时长"+this.kgdy.bdsc_dc+"分钟。"
				}else{
					this.dc_end=this.kgdy.g_45+"G开关电源"+this.number_dianchi+"（业务："+this.kgdy.yw+"),负载:"
					+this.kgdy.fz +"V" +"，品牌："+this.kgdy.ppxh_kgdy+"、生产日期："
					+this.kgdy.scrq_kgdy+"年、模块数："+this.kgdy.mks+"个,下挂"+this.kgdy.sl_dc
					+"组"+this.kgdy.scrq_dc+"年"+this.kgdy.ppxh_dc+this.kgdy.dcrl_dc+"Ah"+this.kgdy.dczl+"电池。备电时长"+this.kgdy.bdsc_dc+"分钟。"
				}
			}else if(this.kgdy.beidian==="无备电"){
				if(this.kgdy.g_45==="4"){
					this.dc_end=this.kgdy.g_45+"G开关电源"+this.number_dianchi+"（业务："+this.kgdy.yw+"),负载:"
						+this.kgdy.fz +"V" +"，品牌："+this.kgdy.ppxh_kgdy+"、生产日期："
					+this.kgdy.scrq_kgdy+"年、模块数："+this.kgdy.mks+"个,无备电。111"
				}else{
					this.dc_end=this.kgdy.g_45+"G开关电源"+this.number_dianchi+"（业务："+this.kgdy.yw+"),总负载："
					+this.kgdy.fz +"V，5G负载："+this.kgdy.fz_5 +"V，品牌："
					+this.kgdy.ppxh_kgdy+"、生产日期："
					+this.kgdy.scrq_kgdy+"年、模块数："+this.kgdy.mks+"个,无备电。"
				}
				
			}else{
				this.dc_end="";
			}
			if(this.dc_end!=""){
				this.title_button_end="确认完毕，已自动添加于下方";
				this.title_error="title_success"
				this.$emit('callback',this.dc_end);
			}else{
				this.title_button_end="请确保信息填写完成";
				this.title_error="title_error";
			}
			
		}
	}
	
}
</script>

<style>
	.css_dainchi_all{
		border: #000000 1rpx solid;
		margin: 15rpx;
		padding-top: 15rpx;
		padding-bottom: 15rpx;
	}
	.css_dainchi_view{
		margin-left: 15rpx;
		display: flex;
	}
	.css_dianchi_input{
		border:#fff 1px solid ;
		border:#000 1px solid ;
		width: 340rpx;
		font-size: 30rpx;
		margin-right: 10rpx;
		padding-left: 10rpx;
	}
	.css_button_down{
		background-color: #00aaff;
		display: flex;
		margin-left: 0;
		margin-right: 0;
		width: 130rpx;
		height: 60rpx;
		font-size: 30rpx;
		text-align: center;
		justify-content: center;
	},
	.css_button_up{
		background-color: #f5f5f5;
		display: flex;
		margin-left: 0;
		margin-right: 0;
		width: 130rpx;
		height: 60rpx;
		font-size: 30rpx;
		text-align: center;
		justify-content: center;
	}
	.title_success{
		background-color: #ececec;
	}
	.title_error{
		color:#fff;
		background-color: #ff0000;
	}
</style>

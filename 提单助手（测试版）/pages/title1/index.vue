<template>
	<view class="css_title_all">
		<view class="css_view">
			提单类型:<input class="input_yys" v-model="tdlx"/>
		</view>
		<view class="css_view">
			<text> 站点信息:</text>
			<view>
			<button :class="button_1" @click="jifangzhandian">房</button>
			<button :class="button_2" @click="jiguizhandian">柜</button>
			<button :class="button_12" @click="guifang">柜+房</button>
			</view>
			<!-- <input class="select_jifang" @change="jifang_change($event)">
				<option v-for="item in jifang" :value="item.text">{{item.text}}</option>
				<!-- <option value="机房站点">机房站点</option>
				<option value="机柜站点">机柜站点</option>
			</input> -->
			<view class="css_view" v-show="isjifang">
				<text>机房面积:</text>
				<input class="input_all" v-model="area"></input>
				<text>m²</text>
			</view>
		</view>
		<text class="css_view"> 运营商情况：</text>
			<view class="css_view">
				<text>在用:</text>
				<input type="number" class="input_all" v-model="yys"></input>
				<text>家运营商，</text>
				<input class="input_yys" v-model="yys_str"></input>
			</view>
		<text class="css_view"> 现场设备情况：</text>
		<view>
			<view class="css_view_1" v-if="isjigui">
				<input type="number" class="input_all" v-model="jigui"></input>
				<text>台机柜</text>
			</view>
			<view class="css_view_1">
				<input type="number" class="input_all" v-model="kgdy"></input>
				<text>台开关电源</text>
			</view>
			<view class="css_view_1">
				<input type="number" class="input_all" v-model="kt"></input>
				<text>台空调</text>
			</view>
			<view class="css_view_1">
				<input type="number" class="input_all" v-model="dc"></input>
				<text>组电池</text>
			</view>
			<view class="css_view_1">
				<view class="css_view_1">
					<view class="css_view_2" >
						<!-- <select class="select_dianchi" v-model="dianchi_1" @change="jifang_change_dc">
							<option v-for="item in dianchi" :value="item.text">{{item.text}}</option>
						</select> -->
						<view>
							<button :class="button_3" @click="qiansuan_1">铅酸</button>
							<button :class="button_4" @click="tieli_1">铁锂</button>
							<button :class="button_5" @click="tici_1">梯次</button>
						</view>
						<input type="number" class="input_all" v-model="dc_1"></input>
						<text>组</text>
					</view>
					<view class="css_view_2" >
						<!-- <select class="select_dianchi" v-model="dianchi_2" @change="jifang_change_dc_1">
							<option v-for="item in dianchi" :value="item.text">{{item.text}}</option>
						</select> -->
						<view>
							<button :class="button_6" @click="qiansuan_2">铅酸</button>
							<button :class="button_7" @click="tieli_2">铁锂</button>
							<button :class="button_8" @click="tici_2">梯次</button>
						</view>
						<input type="number" class="input_all" v-model="dc_2"></input>
						<text>组</text>
					</view>
				</view>
			</view>
		</view>
		<button :class="error" @click="btn_click">{{button_text}}</button>
	</view>
</template>

<script>
	export default {
		data(){
			return{
				tdlx:"xx投诉",
				button_text:"编写完成请点击",
				error:"success",
				yys:"",//几家运营
				yys_str:"",//运营商详情
				area:"",//机房面积
				jigui:"",//机柜
				kgdy:"",//开关电源
				dc:"",//电池
				dc_1:"",//电池1的几组
				dc_2:"",//铅酸2几组
				kt:"",//空调
				jifang_1:"",//机房还是机柜返回值
				dianchi_1:"",//电池种类
				dianchi_2:"",//电池种类2
				jifang_end:"",//最后返回的语句
				isjifang:false,//是否是机房站点
				isjigui:false,
				button_style:1,
				button_1:"button_up",//控制按钮1点击后的颜色
				button_2:"button_up",//控制按钮2点击后的颜色
				button_12:"button_up",//控制按钮2点击后的颜色
				button_3:"button_up",//控制按钮3点击后的颜色
				button_4:"button_up",//控制按钮4点击后的颜色
				button_5:"button_up",//控制按钮5点击后的颜色
				button_6:"button_up",//控制按钮6点击后的颜色
				button_7:"button_up",//控制按钮7点击后的颜色
				button_8:"button_up",//控制按钮8点击后的颜色
				jifang:[
					{id:1,text:"机柜站点"},
					{id:2,text:"机房站点"}
				],
				dianchi:[
					{id:0,text:""},
					{id:1,text:"铁锂"},
					{id:2,text:"铅酸"},
					{id:3,text:"梯次"},
				]
				
			}
		},

		methods:{
			jifangzhandian(){
				this.button_1="button_down"
				this.button_2="button_up"
				this.button_12="button_up"
				this.jifang_1="机房站点";
				if(this.jifang_1==="机柜站点"){
					this.isjigui=true;
					this.isjifang=false;
				}
				else if(this.jifang_1==="机房站点"){
					this.isjigui=false;
					this.isjifang=true;
				}
				console.log(this.jifang_1);
			},
			jiguizhandian(){
				this.button_1="button_up"
				this.button_2="button_down"
				this.button_12="button_up"
				this.jifang_1="机柜站点";
				if(this.jifang_1==="机柜站点"){
					this.isjigui=true;
					this.isjifang=false;
				}
				else if(this.jifang_1==="机房站点"){
					this.isjigui=false;
					this.isjifang=true;
				}
				console.log(this.jifang_1);
			},
			guifang(){
				this.button_1="button_up"
				this.button_2="button_up"
				this.button_12="button_down"
				this.jifang_1="机房+机柜站点";
				if(this.jifang_1==="机房+机柜站点"){
					this.isjigui=true;
					this.isjifang=true;
				}
				console.log(this.jifang_1);
			},
			qiansuan_1(){
				this.dianchi_1="铅酸"
				this.button_3="button_down"
				this.button_4="button_up"
				this.button_5="button_up"
				console.log("第一组电池："+this.dianchi_1)
			},
			tieli_1(){
				this.dianchi_1="铁锂"
				this.button_3="button_up"
				this.button_4="button_down"
				this.button_5="button_up"
				console.log("第一组电池："+this.dianchi_1)
			},
			tici_1(){
				this.dianchi_1="梯次"
				this.button_3="button_up"
				this.button_4="button_up"
				this.button_5="button_down"
				console.log("第一组电池："+this.dianchi_1)
			},
			qiansuan_2(){
				this.dianchi_2="铅酸"
				this.button_6="button_down"
				this.button_7="button_up"
				this.button_8="button_up"
				console.log("第二组电池："+this.dianchi_2)
			},
			tieli_2(){
				this.dianchi_2="铁锂"
				this.button_6="button_up"
				this.button_7="button_down"
				this.button_8="button_up"
				console.log("第二组电池："+this.dianchi_2)
			},
			tici_2(){
				this.dianchi_2="梯次"
				this.button_6="button_up"
				this.button_7="button_up"
				this.button_8="button_down"
				console.log("第二组电池："+this.dianchi_2)
			},
			jifang_change_dc(){
				console.log(this.dianchi_1)
			},
			jifang_change_dc_1(){
				console.log(this.dianchi_2)
			},
			btn_click(){
				if(this.jifang_1==="机房站点"&&this.dc_1!=""&&this.dc_2==""){
					this.jifang_end="【"+this.tdlx+"】"+"该站点为"+this.jifang_1+"。机房面积约为："+this.area+"平。"+
					"在用"+this.yys+"家运营商（"+this.yys_str+"）。"+"现场"+this.kgdy+"台开关电源，"
					+this.kt+"台空调，"+this.dc+"台电池（"+this.dianchi_1+this.dc_1+"组）。"
				}
				else if(this.jifang_1==="机房站点"&&this.dc_1!=""&&this.dc_2!=""){
				this.jifang_end="【"+this.tdlx+"】"+"该站点为"+this.jifang_1+"。机房面积约为："+this.area+"平。"+
				"在用"+this.yys+"家运营商（"+this.yys_str+"）。"+"现场"+this.kgdy+"台开关电源，"
					+this.kt+"台空调，"+this.dc+"台电池（"+this.dianchi_1+this.dc_1+"组，"+this.dianchi_2+this.dc_2+"组）。"
					
				}
				else if(this.jifang_1==="机柜站点"&&this.jigui!=""&&this.dc_1!=""&&this.dc_2==""){
					this.jifang_end="【"+this.tdlx+"】"+"该站点为"+this.jifang_1+"。"+
					"在用"+this.yys+"家运营商（"+this.yys_str+"）。"+"现场"+this.kgdy+"台开关电源，"
					+this.kt+"台空调，"+this.dc+"台电池（"+this.dianchi_1+this.dc_1+"组）。"
				
				}
				else if(this.jifang_1==="机柜站点"&&this.jigui!=""&&this.dc_1!=""&&this.dc_2!=""){
				this.jifang_end="【"+this.tdlx+"】"+"该站点为"+this.jifang_1+"。"+
				"在用"+this.yys+"家运营商（"+this.yys_str+"）。"+"现场"+this.jigui+"台机柜，"+this.kgdy+"台开关电源，"
					+this.kt+"台空调，"+this.dc+"台电池（"+this.dianchi_1+this.dc_1+"组，"+this.dianchi_2+this.dc_2+"组）。"
				
				}
				else if(this.jifang_1==="机房+机柜站点"&&this.jigui!=""&&this.dc_1!=""&&this.dc_2==""){
					this.jifang_end="【"+this.tdlx+"】"+"该站点为"+this.jifang_1+"。机房面积约为："+this.area+"平。"+
					"在用"+this.yys+"家运营商（"+this.yys_str+"）。"+"现场"+this.kgdy+"台开关电源，"
					+this.kt+"台空调，"+this.dc+"台电池（"+this.dianchi_1+this.dc_1+"组）。"
				
				}
				else if(this.jifang_1==="机房+机柜站点"&&this.jigui!=""&&this.dc_1!=""&&this.dc_2!=""){
				this.jifang_end="【"+this.tdlx+"】"+"该站点为"+this.jifang_1+"。机房面积约为："+this.area+"平。"+
				"在用"+this.yys+"家运营商（"+this.yys_str+"）。"+"现场"+this.jigui+"台机柜，"+this.kgdy+"台开关电源，"
					+this.kt+"台空调，"+this.dc+"台电池（"+this.dianchi_1+this.dc_1+"组，"+this.dianchi_2+this.dc_2+"组）。"
				
				}
				else{
					this.jifang_end=""
				}
				if(this.jifang_end!=""){
					this.button_text="确认完毕，已自动添加于下方"
					this.error="success";
					this.$emit('callback1',this.jifang_end);
				}
				else{
					this.button_text="请确保信息填写完成"
					this.error="error";
				}
				
			}
		}
	}
</script>

<style>
	.css_title_all{
		border: #000000 1rpx solid;
		margin: 15rpx;
		padding-top: 15rpx;
		padding-bottom: 15rpx;
	}
	.select_jifang{
		width: 200rpx;
		height: 50rpx;
	}
	.css_view{
		margin-left: 15rpx;
		display: flex;
	}
	.css_view_1{
		margin-left: 5%;
		display: flex;
	}
	.css_view_2{
		display: flex;
	}
	.button_down{
		display: flex;
		height: 60rpx;
		width: 150rpx;
		font-size: 10px;
		margin-left: 10rpx;
		background-color: #00aaff;
		color: #fff;
		text-align: center;
	}
	.button_up{
		position: flex;
		height: 60rpx;
		width: 150rpx;
		font-size: 10px;
		margin-left: 10rpx;
		background-color: #ececec;
		text-align: center;
	}
	.input_all{
		border:#fff 1px solid ;
		border:#000 1px solid ;
		width: 70rpx;
		font-size: 30rpx;
		color: #000;
	}
	.input_yys{
		border:#fff 1px solid ;
		border:#000 1px solid ;
		width: 320rpx;
		font-size: 30rpx;
		color: #000;
		padding-left:10rpx ;
	}
	.select_dianchi{
		margin-left: 0%;
		height: 90%;
		font-size:12px;
	}
	.success{
		background-color: #ececec;
	}
	.error{
		color:#fff;
		background-color: #ff0000;
	}
</style>

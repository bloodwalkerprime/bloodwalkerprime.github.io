<template>
	<view>
		<view class="text-area">
			<view class="choose">
				<radio-group>
					<radio @click="zhengzhi_dianchi">电池</radio>
					<radio @click="zhengzhi_dianyuan">电源</radio>
					<radio @click="zhengzhi_kongtiao">空调</radio>
					<radio @click="zhengzhi_FSU">FSU</radio>
					<radio @click="zhengzhi_qita">其他</radio>
				</radio-group>
			</view>
		</view>
		
		<view data-tap-disabled="true">
			<title1 @callback1="callback1"></title1>
		</view>
		<view>
			<view v-if="dianchi_if">
				<dianchi  v-for="index in dianchi_value"  :number="number" @callback="callback"></dianchi>
				<view style="display:flex;">
					<button class="kgdy_index_button" @click="dainchijian">减少开关电源</button>
					<button class="kgdy_index_button" @click="dainchijia">增加开关电源</button>
				</view>
			</view>
			
			<dianyuan v-if="dianyuan_if"></dianyuan>
			
			<kongtiao v-if="kongtiao_if" @kongtiao_end="kongtiao_end"></kongtiao>
			<view style="border: #000 1rpx solid;margin: 10rpx;">
				<view style="display: flex;">
					<button class="kgdy_index_button_2" @click="all_cancel">清除</button>
				</view>
				<label>请加上站名和站址id后直接复制整段话</label>
				<textarea  name="" id="" cols="30" rows="10" style="border: #000 1rpx solid;width:97%;height: 800rpx;padding: 12rpx;" v-model="xuqiu_end"></textarea>
			</view>
		</view>
	</view>
</template>

<script>
	import dianchi from '../dianchi/index.vue'
	import dianyuan from '../dinayuan/index.vue'
	import title1 from '../title1/index.vue'
	import kongtiao from '../kongtiao/index.vue'
	export default {
		components: {
			title1,dianchi,dianyuan,kongtiao
		},
		data() {
			return {
				number:1,
				dianchi_value:[{}],//开关电源的数量
				kongtiao_value:[{}],//空调的数量
				zzlx:"",//整治类型
				dianchi_if:false,
				dianyuan_if:false,
				kongtiao_if:false,
				FSU_if:false,
				qita_if:false,
				selectClassEnd:"NONE",//默认选择
				select_class_id:"",//类别id提交报名需要
				xuqiu_end:"站名+站址（需要队长手动填写）"
			}
		},
		created() {
		},
		methods: {
			zhengzhi_dianchi(){
				this.zzlx="电池整治";
				this.dianchi_if=true;
				this.dianyuan_if=false;
				this.kongtiao_if=false;
				this.FSU_if=false;
				this.qita_if=false;
			},
			zhengzhi_dianyuan(){
				this.zzlx="电源整治";
				this.dianchi_if=false;
				this.dianyuan_if=true;
				this.kongtiao_if=false;
				this.FSU_if=false;
				this.qita_if=false;
			},
			zhengzhi_qita(){
				this.zzlx="其他整治";
				this.dianchi_if=false;
				this.dianyuan_if=false;
				this.kongtiao_if=false;
				this.FSU_if=false;
				this.qita_if=true;
			},
			zhengzhi_FSU(){
				this.zzlx="FSU整治";
				this.dianchi_if=false;
				this.dianyuan_if=false;
				this.kongtiao_if=false;
				this.FSU_if=true;
				this.qita_if=false;
				
			},
			zhengzhi_kongtiao(){
				this.zzlx="空调整治";
				this.dianchi_if=false;
				this.dianyuan_if=false;
				this.kongtiao_if=true;
				this.FSU_if=false;
				this.qita_if=false;
			},
			
			dainchijia(){
				console.log("增加一个开关电源");
				this.dianchi_value.push({});
				this.number+=1;
			},
			dainchijian(){
				console.log("减少一个开关电源")
				this.dianchi_value.pop({});
				this.number-=1;
			},
			callback1:function(jifang_end){
				this.xuqiu_end=this.xuqiu_end.concat(jifang_end)
			},
			callback:function(dc_end){
				this.xuqiu_end=this.xuqiu_end.concat(dc_end)
			},
			all_cancel(){
				this.xuqiu_end="站名+站址（需要队长手动填写）"
			},
			kongtiao_end(e){
				this.xuqiu_end=this.xuqiu_end.concat(e)
			},
			textarea_end(){
				
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		/* align-items: center; */
		justify-content: center;
	}


	.text-area {
		display: flex;
		padding-left:10% ;
		flex-direction: column;
		/* align-items: center; */
		justify-content: center;
	}
	.choose{
		font-size: 45rpx;
		font-weight: 200;
	}
	.scc_select{
		margin-top:20rpx ;
		width: 400rpx;
		height: 60rpx;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
	.kgdy_index_button{
		width: 200rpx;
		height: 50rpx;
		font-size: 10px;
	}
	.kgdy_index_button_2{
		width: 300rpx;
		height: 100rpx;
		font-size: 20px;
		font-weight: 2px;
	}
</style>

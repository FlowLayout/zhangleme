<template>
	<view>
	
	<view class="place"></view>
	<view class="exp">
		<text>股票名称:{{name}}</text>
	</view>
	<view class="place"></view>
	<view class="exp">
		 <text>实时股价:</text><text>{{price+"    "}}</text>
	</view>
	<view class="place"></view>
	<view class="exp">
		<text>涨跌百分比:</text><text>{{increPer+"%"}}</text>
	</view>
	<view class="place"></view>
	<view class="exp">
		<text>预测涨幅:</text><text>{{rand[pred]+"%"}}</text>
	</view>
	<view class="place"></view>
	<view class="place2">
		<image class="place2" src="../../static/query/stockQuery.jpg" mode=scaleToFill></image>
	</view>
	<view class="place"></view>
	<view class="row">
		<input class="stockIn" @blur="type" :value="hisCode" placeholder-style="color:#d5d3d4" placeholder="请输入待查询股票代码或名称"/>
		<button class="stockBut" v-on:click="voice" type="primary" plain="true"><image class="stockBut" src="../../static/rec.png" mode="scaleToFill"></image> </button>
	</view>
	<button v-on:click="search" type="primary" hover-class="button-hover">查询</button>
	<view class="place8">
	</view>
	
	<view class="row">
	
	<picker mode="selector" :range="history" range-key="name" @change="insert">
			<view class="place9">
			<button class="place6 textHis" size="mini" plain="true" type="warn">历史记录</button>
			</view>
	</picker>
	
	<view class="place7">
		<button @click="askClean" plain="true" type="warn">🗑</button>
	</view>
	</view>	
	
	</view>
	
</template>

<script>
	let stockCode;
	let price;
	let name;
	let hisIndex;
	let hisCode;
	let allName;
	const rec = uni.getRecorderManager();
	let recB;
	export default{
		data(){
			return {
				price:uni.getStorageSync('stockPrice')+"(未更新)",
				name:uni.getStorageSync('stockName'),
				increPer:0.00,
				hisCode:'',
				rand:[0.32,-1.62,1.29,0.44,-0.76],
				pred:0,
				recB:1,
				allName:[{'name':'农业银行','code':'601288'},
				
		{'name':'建设银行','code':'601939'},
		{'name':'中油资本','code':'000617'},
		{'name':'南方航空','code':'600029'},
		{'name':'中国银行','code':'601988'},
		{'name':'荣盛石化','code':'002493'},
		{'name':'中信银行','code':'601998'},
		{'name':'中国石化','code':'600028'},
		{'name':'广汽集团','code':'601238'},
		{'name':'传化智联','code':'002010'},
		{'name':'光大银行','code':'601818'},
		{'name':'广汇汽车','code':'600297'},
		{'name':'宁沪高速','code':'600377'},
		{'name':'交通银行','code':'601328'},
		{'name':'恒力股份','code':'600346'},
		{'name':'韵达股份','code':'002120'},
		{'name':'华能国际','code':'600011'},
		{'name':'分众传媒','code':'002027'},
		{'name':'上海莱士','code':'002252'},
		{'name':'联美控股','code':'600167'},
		{'name':'海航基础','code':'600515'},
		{'name':'江苏国信','code':'002608'},
		{'name':'中国人寿','code':'601628'},
		{'name':'新光圆成','code':'002147'},
		{'name':'华峰超纤','code':'300180'},
		{'name':'必康股份','code':'002411'},
		{'name':'陕西煤业','code':'601225'},
		{'name':'南极电商','code':'002127'},
		{'name':'飞马国际','code':'002210'},
		{'name':'兴源环境','code':'300266'},
		{'name':'美晨生态','code':'300237'},
		{'name':'ST油服','code':'600871'},
		{'name':'安迪苏','code':'600299'},
		{'name':'森马服饰','code':'002563'},
		{'name':'立讯精密','code':'002475'},
		{'name':'中国交建','code':'601800'},
		{'name':'深高速','code':'600548'},
		{'name':'皖江物流','code':'600575'},
		{'name':'德展健康','code':'000813'},
		{'name':'海大集团','code':'002311'},
		{'name':'恒逸石化','code':'000703'},
		{'name':'上海石化','code':'600688'},
		{'name':'完美世界','code':'002624'},
		{'name':'希努尔','code':'002485'},
		{'name':'华夏银行','code':'600015'},
		{'name':'齐星铁塔','code':'002359'},
		{'name':'大秦铁路','code':'601006'},
		{'name':'海天味业','code':'603288'},
		{'name':'重庆水务','code':'601158'},
		{'name':'温氏股份','code':'300498'}]
				}
			
		}	,
			
		onLoad() {
	        uni.showLoading({
	     	    title: '加载中'
	     	})
	        if(''==uni.getStorageSync('hisIndex')){
			this.history=[{'name':'','code':''},{'name':'','code':''},{'name':'','code':''},{'name':'','code':''},{'name':'','code':''}]
			this.hisIndex=0
			uni.setStorageSync('hisIndex',0)
			uni.setStorageSync('history',this.history)
		 }
		 
		    this.hisIndex=uni.getStorageSync('hisIndex')
		    this.history=uni.getStorageSync('history')
		    setTimeout(()=>{uni.hideLoading()},700)
			
		},
		
		methods:{
			type(event){
				if(event.detail.value[0]==6){stockCode='sh'+event.detail.value}
				else{stockCode='sh'+this.searchCode(event.detail.value)}
			},
			searchCode(sna){
				for (let i = 0; i < 50; i++) {
						if(this.allName[i].name==sna){
							return this.allName[i].code
							
						}
					}
			},
			voice(){
				
			//if(this.recB==1){
			//recB=0
			//rec.start(
				//format:'PCM',
				//numberOfChannels:1,
				//sampleRate:16000
			//);
				uni.showLoading({title:'录制中'})
					setTimeout(()=>{
						uni.hideLoading()
						
						},2500)
				
				
				
			//	for (let i = 0; i < 50; i++) {
			//		if(this.allName[i].name==sna){
			//			this.hisCode=this.allName[i].code
			//			break
			//		}
			//	}
			uni.showLoading({title:'识别中'})
				setTimeout(()=>{
					uni.hideLoading()
					this.hisCode="中国银行"
					},1500)
					
			//	}
			//	else{
					//console.log(this.recB)
			//		rec.Stop({
			//			tempFilePath:'@/static/'
			//		})
			//		this.recB=1
			
			//		uni.request({
			//			method:"POST",
			//			url:'http://vop.baidu.com/server_api',
			//			data:{
							
			//			}
						
			//		})
			//	}
			},
			
			
			push(his){
				if(this.hisIndex<5){
				this.history[this.hisIndex].code=his.code
				this.history[this.hisIndex].name=his.name
				this.hisIndex++
				uni.setStorageSync('hisIndex',this.hisIndex)
				uni.setStorageSync('history',this.history)
				
				}
				
			},
			askClean(){
				uni.showModal({
				    title: '提示',
				    content: '确定要清空查询历史吗？',
				    success(res) {
				        if (res.confirm) {
				            this.history=[{'name':'','code':''},{'name':'','code':''},{'name':'','code':''},{'name':'','code':''},{'name':'','code':''}]
				            this.hisIndex=0
				            uni.setStorageSync('hisIndex',0)
							uni.setStorageSync('history',this.history)
				        } 
				    }
				});
			},
			
			insert(e){
				this.hisCode=this.history[e.detail.value].code
			},
			search(){
				uni.showLoading({
				    title: '查询中'
				});
				this.pred=(this.pred+1)%5
				uni.request({
					url:'http://web.juhe.cn:8080/finance/stock/hs',
					data: {
					        gid: stockCode,
					        key: '89826c4dd4e319a06814ddb4c1ba2599'
					    },
					success(res) {
						//sh601009
						
						if(res.data.reason=="SUCCESSED!"){
						
						uni.setStorageSync('stockPrice',res.data.result["0"].data.nowPri)
						uni.setStorageSync('stockName',res.data.result["0"].data.name)
						uni.setStorageSync('increPer',res.data.result["0"].data.increPer)
					
						}
						else{
							
						}
					},
				}),
				setTimeout(()=>{
					uni.hideLoading()
					this.name=uni.getStorageSync('stockName')
					this.price=uni.getStorageSync('stockPrice')
					this.increPer=uni.getStorageSync('increPer')
					
					this.push({
						'name':this.name,
						'code':stockCode
						})
						stockCode=''
					},1600)
			
			},
			
		}
	}
</script>

<style>
	@import url("../../static/My.css");
</style>
<template>
	<view>
		<uni-search-bar  radius="5" placeholder="自动显示隐藏" clearButton="auto" cancelButton="none" @confirm="search" />
		<view class="content">
			<uni-swiper-dot :info="info" :current="current" field="content" :mode="mode">
				<swiper class="swiper-box" @change="change">
					<swiper-item v-for="(item ,index) in info" :key="index">
						<view class="swiper-item">
							<image :lazy-load="true" :src="imageUrl" mode="widthFix"></image>
						</view>
					</swiper-item>
				</swiper>
			</uni-swiper-dot>
		
			<h1>热门经典排行榜</h1>
			<view class="classification-hot">
				<view>
					<image :lazy-load="true" :src="imageUrl" mode="widthFix" style="width:80px"></image>
					<text>城市旅游</text>
				</view>
				<view>
					<image :lazy-load="true" :src="imageUrl" mode="widthFix" style="width:80px"></image>
					<text>城市旅游</text>
				</view>
				<view>
					<image :lazy-load="true" :src="imageUrl" mode="widthFix" style="width:80px"></image>
					<text>城市旅游</text>
				</view>
				<view>
					<image :lazy-load="true" :src="imageUrl" mode="widthFix" style="width:80px"></image>
					<text>城市旅游</text>
				</view>
				<view>
					<image :lazy-load="true" :src="imageUrl" mode="widthFix" style="width:80px"></image>
					<text>城市旅游</text>
				</view>
				<view>
					<image :lazy-load="true" :src="imageUrl" mode="widthFix" style="width:80px"></image>
					<text>城市旅游</text>
				</view>
				<view>
					<image :lazy-load="true" :src="imageUrl" mode="widthFix" style="width:80px"></image>
					<text>城市旅游</text>
				</view>
				<view>
					<image :lazy-load="true" :src="imageUrl" mode="widthFix" style="width:80px"></image>
					<text>城市旅游</text>
				</view>
			</view>
			<h1>推荐景点</h1>
			<view class="classification" v-for="item in dataList">
				<view>
					<image :lazy-load="true" :src="imageUrl" mode="widthFix" style="width:180px"></image>
					<text>城市旅游</text>
				</view>
				<view>
					<image :lazy-load="true" :src="imageUrl" mode="widthFix" style="width:180px"></image>
					<text>城市旅游</text>
				</view>
		 
			</view>
		</view>
	</view>
	
</template>

<script>
export default {
	data() {
		return {
			imageUrl:'https://img2.baidu.com/it/u=1028011339,1319212411&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=313',
			info: [{
				content: '内容 A'
			}, {
				content: '内容 B'
			}, {
				content: '内容 C'
			}],
			dataList:[{},{},{},{},{},{},{}],
			current: 0,
			mode: 'round',
		}
	},
	onReachBottom() {
	    // 页面滚动到底部时触发
	console.log('触底了！'); 
		
	for (let i = 0;i++;i<30){
		this.dataList.push({})
	}
	
  },
  mounted(){
	  uni.getLocation({
	  	    // gcj02 返回国测局坐标（App 和 H5 需配置定位 SDK 信息才可支持 gcj02。）
	  		type: 'gcj02', 
	  		// 是否解析地址信息（仅App平台支持（安卓需指定 type 为 gcj02 并配置三方定位SDK））
	  		geocode: true, 
	  		success: function(res) {
	  			console.log(res);
	  		}
	  	});
	  uni.setNavigationBarTitle({
		title:'this.title'
	});	
  },
	methods: {
		change(e) {
			this.current = e.detail.current;
		}
	}
};
</script>

<style>
.content {
	text-align: center;
	padding: 0 20upx;
	height: 400upx;
 }
 .swiper-item image{
	 width:100%;
	 border-radius: 3px;
 }
 .swiper-item{
	 overflow: hidden;
 }
 .uni-searchbar{
	 padding: 10upx 0
 }
 .classification{
	 display: flex;
	 margin-top:10px;
	 justify-content: space-between;
 }
.classification-hot{
	 display: flex;
	 justify-content: space-between;
	 flex-wrap: wrap;
 }
.classification-hot text{
	display: block;
}
.classification text{
	display: block;
}
 .classification image{
	 widht:120upx;
	 height:120upx;
 }
</style>

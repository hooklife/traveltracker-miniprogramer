<template>
<view>
    <view class="page-body">
		<button @click="getLocationTap">+</button>
        <view class="page-map-box">
            <map style="width: 750rpx; height: 600rpx;" 
				ref="mapHtml"
				  id="map"
				  :latitude="latitude" 
				  :show-location="true"
				  :longitude="longitude" 
				  :scale="scale"
				  :polyline="polyline"
				  :markers="markers"
             ></map>
        </view>
		<div class="list-box-content">
			<uni-swipe-action-item v-for="(item,i) in 12" :key="item" class="list-box">
				<view class="content-box" @click="getMap()">
					<text class="content-text">{{i+1}} . 景点详情</text>
				</view>
				<template v-slot:right>
					<view class="slot-button" @click="bindClick({position:'right',content:{text:'删除'}})"><text class="slot-button-text">删除</text></view>
				</template>
			</uni-swipe-action-item>
		</div>
		
      <!-- <view class="btn-position">
         <button type="default" @tap="getLocationTap">获取定位</button>
      </view> -->
    </view>
</view>
</template>

<script>
export default {
    data(){
        return {
            latitude: 32.131962,
            longitude: 119.433854,
            scale: 14, // 设置地图的缩放级别
			_mapContext: null,
			polyline:[{  
            points: [{  
                    latitude: 32.131962,  
                    longitude: 119.433854  
                }, 
				{ latitude: 32.131962,
                   longitude: 119.433854,},
                {  
                    latitude: 32.131962,  
                    longitude: 119.436854  
                }  
            ],  
            color: '#22ac38',  
            width: 3,   
        }, ],
            markers: [ // 设置标记点
               {
                   id:1001,
                   width:35,
                   height:50,
                   latitude: 32.131962,
                   longitude: 119.433854,
                   // iconPath: '../../static/weizhi.png',
				     label: {
						 width: 50,
						 height: 30,
						 borderWidth: 1,
						 borderRadius: 10, 
						 bgColor: '#ffffff',
						 content: `label ${'n' + 1}`
					 }
               },
			   {
			       id:1001,
			       width:35,
			       height:50,
			       latitude: 32.131962,
			       longitude: 119.436854,
			       // iconPath: '../../static/weizhi.png',
				     label: {
						 width: 60,
						 height: 30,
						 borderWidth: 1,
						 borderRadius: 10,
						 bgColor: '#ffffff',
						 content: `金勺子饭店`
					 }
			   },
           ],
        }
    },
	onReady() {
	  this._mapContext = uni.createMapContext("map", this);
	},
    methods:{
		getMap(){
			// this.latitude = 32.131962
			// this.longitude = 119.433854
			// console.log(this.latitude,this.longitude);	
			setTimeout(()=>{
				this._mapContext.moveToLocation({
					latitude: 31.131962,
					longitude: 120.436854,
				})
			},100)
			
			console.log(this._mapContext,this.latitude)
		},
		addTidy(){
			
		},
        getLocationTap(){
			let that=this;
			uni.getLocation({ 
			  type: 'gcj02', 
			  success: function (res) { 
				  that._mapContext.moveToLocation({
				  	latitude: res.latitude,
				  	longitude: res.longitude,
				  })
	 
				console.log(res)
			  }, 
			  fail: function (res) { 
				console.log('获取位置信息失败', res); 
			  } 
			})
        }
    }
}
</script>
<style scoped>
	.page-map-box{
		width: 750rpx; 
		/* height: 600rpx; */
	}
	.list-box{
		height: 40rpx;
		line-height: 40rpx;
		border-bottom: 1px solid #ddd;
		padding: 40rpx 20rpx;
		display: block;
	}
	.list-box-content{
		height: 700rpx;
		overflow: auto;
	}
	.slot-button{
		/* background-color: red; */
		color:red;
	}
	.btn-position{
		margin-top: 10rpx;
	}
</style>
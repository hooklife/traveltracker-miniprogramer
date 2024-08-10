<template>
<view>
    <view class="page-body">
        <view class="page-map-box">
            <map style="width: 750rpx; height: 600rpx;" 
              :latitude="latitude" 
              :longitude="longitude" 
              :scale="scale"
              :markers="markers"
             ></map>
        </view>
      <view class="btn-position">
         <button type="default" @tap="getLocationTap">获取定位</button>
      </view>
    </view>
</view>
</template>

<script>
export default {
    data(){
        return {
            latitude: '',
            longitude: '',
            scale: 14, // 设置地图的缩放级别
            markers: [ // 设置标记点
                {  
                    id:1001,
                    width:50,
                    height:50,
                    latitude: this.latitude*1,
                    longitude: this.longitude*1,
                    iconPath: '../../static/weizhi.png',
                },
           ],
        }
    },
    methods:{
        getLocationTap(){
        let that=this;
        uni.getLocation({ 
          type: 'gcj02', 
          success: function (res) { 
            console.log('经度：' + res.longitude);
            console.log('纬度：' + res.latitude); 
            that.latitude = res.latitude
            that.longitude= res.longitude
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
		width: 750rpx; height: 600rpx;
	}
	.btn-position{
		margin-top: 10rpx;
	}
</style>
<template>
	<view class="nav-bar">
		<view class="nav-bar-top" > 
		  <view :style="{height:setNavHeight+'rpx'}"></view> <!-- 占位元素 手机app状态栏的高度-->
		  <view class="nav-bar-content" :style="{marginRight:marginRight+'rpx'}">
			  <uni-icons type="search" size="18" color="#999"></uni-icons>
			  <view class="nav-bar-search">
				  输入文章标题进行搜索
			  </view>
		  </view>
		</view>
		<view :style="{height:80+setNavHeight+'rpx'}"></view>
	</view>
</template>

<script>
	export default {
		name:"NavBar",
		data() {
			return {
			   setNavHeight:20,//导航的高度
			   marginRight:0,
			};
		},
		created(){
			this.getnavInfoSync();//获取导航信息
		},
		methods:{
			getnavInfoSync(){   //小程序跟app是有状态栏的，h5没有 所以要做特殊处理，动态设置高度
				const res = uni.getSystemInfoSync(); //获取系统信息同步接口
				res.statusBarHeight&&(this.setNavHeight = res.statusBarHeight*2);//获取状态栏的高度 ，小程序跟app是有状态栏的，h5没有 
				console.log(this.setNavHeight);
				//只有微信小程序才会执行下面代码
				// #ifdef MP-WEIXIN    
				   let menuButtonInfo = uni.getMenuButtonBoundingClientRect(); //获取小程序里面胶囊按钮的信息
				   this.setNavHeight = menuButtonInfo.top * 2;
				   this.marginRight = menuButtonInfo.width*2;
				   console.log(this.setNavHeight,menuButtonInfo,this.marginRight)
				// #endif
			}
		}
	}
</script>

<style lang="scss" scoped>
 .nav-bar-top{
	 width:100%;
	 padding:0rpx 30rpx 20rpx;
	 background:$base-color;
	 position:fixed;
	 top:0;
	 left:0;
	 box-sizing: border-box;
	 .nav-bar-content{
		 @include flex("flex-start"); //引入scss语法
		 background:#fff;
		 border-radius: 30rpx;
		 height:60rpx;
		 padding-left: 20rpx;
		 box-sizing: border-box;
	 }
	 .nav-bar-search{
		 font-size:28rpx;
		 color:#999;
		 // height:100%;
		 padding-left:10rpx;
	 }
 }
</style>

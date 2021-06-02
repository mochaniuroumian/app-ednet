<template>
  <view class="container">
	<view class="content">
		<view class="logo"><image mode="aspectFit" :src="imageUrllogo"></image></view>
		<view class="colorwhite bigfont ede">e德互联</view>
		<view class="colorwhite titleright">
			<view class="connull"></view>
			<text>云端共享.服务升级</text>
		</view>
		<view class="uni-padding-wrap service">
            <view class="page-section swiper">
                <view class="page-section-spacing">
                    <swiper class="swiper service-swiper" circular="true" :current="curDot" @change="swiperChange">
                        <swiper-item>
                            <view class="swiper-item">
								<view class="colorwhite bigfont">重磅推出</view>
								<view class="colorwhite swiper-appcont">
			                      <image mode="aspectFit" :src="imageUrl25"></image>
			                      <view><text>微信小程序</text><text>注册.开发.代维</text></view>
		                        </view>
								<button type="primary" open-type="contact">免费升级</button>
								<!-- <button type="primary" @tap="call('4006511688')">免费升级</button> -->
							</view>
                        </swiper-item>
                    </swiper>
                </view>
            </view>
			<!-- <uni-icons class="leftright arrowleft" type="arrowleft" size="50" color="#c7c7c799" @click.stop="leftImg"></uni-icons> -->
			<uni-icons class="leftright arrowleft" type="arrowleft" size="50" color="#c7c7c799"></uni-icons>
            <uni-icons class="leftright arrowright" type="arrowright" size="50" color="#c7c7c799"></uni-icons>
		</view>
		<view class="index-next">
		    <button open-type="getUserInfo" plain="true" @getuserinfo="nextpage">
			  <image mode="aspectFit" :src="imageUrlyou"></image>
		    </button>
		</view>
	</view>
	<image class="background" mode="aspectFill" :src="imageUrlback"></image>
  </view>
</template>

<script>
import {uniIcons} from '@dcloudio/uni-ui'
const app = getApp()
	export default {
		data() {
			return {
				curDot: 0,
				username: '未登录用户',
				userimg: app.globalData.imageUrl + 'logo.png',
				imageUrl25:app.globalData.imageUrl + "Group 25.png",
				imageUrllogo:app.globalData.imageUrl + "logo.png",
				imageUrlyou:app.globalData.imageUrl + "you.png",
				imageUrlback:app.globalData.imageUrl + "background.jpg"
			}
		},
		onLoad: function () {
            uni.showShareMenu({
            withShareTicket:true,
            menus:["shareAppMessage","shareTimeline"]
            })
        },
		methods: {
          swiperChange(e) {
	        this.curDot = e.detail.current;
          },
		  leftImg(){
	        // let num = this.list.length - 1
	        if (this.curDot <= 0) {
		      this.curDot = 2
	        } else {
		      this.curDot--
	        }
          },
          rightImg(){
	        // let num = this.list.length - 1
	        if (this.curDot >= 2) {
		      this.curDot = 0
	        } else {
		      this.curDot++
	        }
          },
		  call(phone){
            uni.makePhoneCall({phoneNumber: phone})
		  },
		  nextpage() {
			uni.getUserInfo({
              success: res => {
                this.username = res.userInfo.nickName
				this.userimg = res.userInfo.avatarUrl
				uni.redirectTo({
					url: '/pages/product/product?name=' + this.username + '&img=' + this.userimg,
				})
              },
			  fail() {
				this.username = '未登录用户'
				this.userimg = app.globalData.imageUrl + 'logo.png'
			  }
			});
		  },
		  //发送给朋友
  onShareAppMessage(res) {
  // 此处的distSource为分享者的部分信息，需要传递给其他人
  let distSource = uni.getStorageSync('distSource');
  if (distSource) {
  return {
  title: 'e德互联欢迎你',
  type: 0,
  path: '/pages/indexmusic/index',
  summary: "",
  imageUrl: "这个是分享图片地址"
  }
  }
  },
  //分享到朋友圈
  onShareTimeline(res) {
  let distSource = uni.getStorageSync('distSource');
  if (distSource) {
  return {
  title: 'e德互联欢迎你',
  type: 0,
  query: 'id=' + distSource, //这个是参数
  summary: "",
  imageUrl: "这个是分享图片地址"
  }
  }
  }
		},
		components: {uniIcons}
	}
</script>

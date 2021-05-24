<template>
  <view class="container">
	<view class="content">
		<view class="logo"><image mode="aspectFit" src="/static/logo.png"></image></view>
		<view class="colorwhite bigfont">e德互联</view>
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
			                      <image mode="aspectFit" src="/static/Group 25.png"></image>
			                      <view><text>微信小程序</text><text>注册.开发.代维</text></view>
		                        </view>
								<button type="primary" @tap="call('4006511688')">免费升级</button>
							</view>
                        </swiper-item>
                        <swiper-item>
                            <view class="swiper-item">B</view>
                        </swiper-item>
                        <swiper-item>
                            <view class="swiper-item">C</view>
                        </swiper-item>
                    </swiper>
                </view>
            </view>
			<uni-icons class="leftright arrowleft" type="arrowleft" size="50" color="#c7c7c799" @click.stop="leftImg"></uni-icons>
            <uni-icons class="leftright arrowright" type="arrowright" size="50" color="#c7c7c799" @click.stop="rightImg"></uni-icons>
		</view>
		<view class="index-next">
		    <button open-type="getUserInfo" plain="true" @getuserinfo="nextpage">
			  <image mode="aspectFit" src="/static/you.png"></image>
		    </button>
		</view>
	</view>
	<image class="background" mode="aspectFill" src="/static/background.jpg"></image>
  </view>
</template>

<script>
import {uniIcons} from '@dcloudio/uni-ui'
	export default {
		data() {
			return {
				curDot: 0,
				username: '未登录用户',
				userimg: '/static/logo.png'
			}
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
				this.userimg = '/static/logo.png'
			  }
			});
		  }
		},
		onShow() {
		    uni.hideTabBar()
		},
		onHide(){
			uni.showTabBar()
		},
		components: {uniIcons}
	}
</script>

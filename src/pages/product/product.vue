<template>
    <view class="container product">
      <view class="hello">
          <view class="user-name">欢迎您，{{uname}}</view>
          <view class="user-img"><image mode="aspectFill" :src="uimg"></image></view>
      </view>
      <view class="product-tab">
          <scroll-view class="scrollbox" scroll-x="true">
              <uni-segmented-control :current="product" :values="productItems" @clickItem="productItem" 
              styleType="button" activeColor="#a9d682"></uni-segmented-control>
          </scroll-view>
          <scroll-view class="pro-content" scroll-y="true">
            <Gongxiang v-if="product === 0"></Gongxiang>
            <Yuming v-if="product === 1"></Yuming>
            <Mailbox v-if="product === 2"></Mailbox>
            <Vhost v-if="product === 3"></Vhost>
            <Wxapp v-if="product === 4"></Wxapp>
          </scroll-view>
      </view>
      <Footer :choose=choose @bottomPro="bottomPro"></Footer>
      <image class="background" mode="aspectFill" :src="imageUrlback"></image>
    </view>
</template>
<script>
import {uniSegmentedControl} from '@dcloudio/uni-ui'
import gongxiang from '@/components/gongxiang'
import yuming from '@/components/yuming'
import mailbox from '@/components/mailbox'
import vhost from '@/components/vhost'
import wxapp from '@/components/wxapp'
import footer from '@/components/footer'
const app = getApp()
export default {
    data() {
        return {
            choose: {
                chooseCard: 0,
                choosePhone: 0,
                addColor: "#8080ff",
                disabled: false
            },
            uname: '未登录用户',
			uimg: app.globalData.imageUrl + 'logo.png',
            imageUrlback:app.globalData.imageUrl + "background.jpg",
            product:0,
            productItems:['共享建站','域名申请','企业邮箱','虚拟主机','微信小程序']
        }
    },
    onLoad(options) {
        this.uname = options.name,
        this.uimg = options.img,
        uni.showShareMenu({
            withShareTicket:true,
            menus:["shareAppMessage","shareTimeline"]
            })
    },
    components: {
        uniSegmentedControl,
        gongxiang,
        yuming,
        mailbox,
        vhost,
        wxapp,
        footer
    },
    methods: {
        productItem(res) {
          this.product = res.currentIndex;
        },
        bottomPro(index) {
          this.product = index
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
    }
}
</script>
<template>
    <view class="container contact">
      <view class="contact-con">
        <view class="map">
          <map :latitude="latitude" :longitude="longitude" :markers="covers"></map>
        </view>
        <view class="contactinfo">
            <view class="erweima">
                <image mode="aspectFit" :src="imageUrler" 
                @click="fullScreen(imageUrler)"></image>
            </view>
            <view class="infos" v-for="(item, index) in infos" :key="index">
                <image mode="aspectFit" :src="item.icon"></image>
                <view class="name"><view class="thename">{{item.name}}</view></view>
                <view class="name-text"><view class="nametext">{{item.nametext}}</view></view>
            </view>
        </view>
      </view>
      <Footer :choose = choose></Footer>
      <image class="background" mode="aspectFill" :src="imageUrlback"></image>
  </view>
</template>

<script>
import footer from '@/components/footer'
const app = getApp()
export default {
    data() {
        return {
            imageUrlback:app.globalData.imageUrl + "background.jpg",
            imageUrler:app.globalData.imageUrl + "erweima.jpg",
            latitude: 39.120615,
            longitude: 117.180686,
            covers: [{
                id:0,
                latitude: 39.120615,
                longitude: 117.180686,
                width: 30,
                height: 42,
                iconPath: app.globalData.imageUrl + 'lucky.png'
            }],
            choose: {
                chooseCard: 0,
                choosePhone: 1,
                addColor: "none",
                disabled: true
            },
            infos: [
                {
                    icon: app.globalData.imageUrl + "gps.png",
                    name: "公司名称：",
                    nametext: "天津市德林瑞泰科技开发有限公司"
                },
                {
                    icon: app.globalData.imageUrl + "site.png",
                    name: "地址：",
                    nametext: "天津市和平区南京路305号经济联合大厦2315-2317"
                },
                {
                    icon: app.globalData.imageUrl + "phone.png",
                    name: "电话：",
                    nametext: "4006511688"
                },
                {
                    icon: app.globalData.imageUrl + "mail.png",
                    name: "邮箱：",
                    nametext: "contact@114mail.com"
                }
            ]
        }
    },
    components: {
        footer
    },
    onLoad: function () {
            uni.showShareMenu({
            withShareTicket:true,
            menus:["shareAppMessage","shareTimeline"]
            })
        },
    methods: {
      fullScreen(img) {
        let imgsArray = []
        imgsArray[0] = img
          uni.previewImage({
            current: 0,
            urls: imgsArray,
            indicator: "none"
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
    }
}
</script>
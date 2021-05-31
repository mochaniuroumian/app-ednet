<template>
  <view class="gongxiang">
      <view class="card" v-for="(item, index) in cardlist" :key="index">
          <view class="cardimg">
            <image mode="widthFix" :src="item.img"></image>
          </view>
          <view class="cardtext" @click="fullScreen(item.httpimg)">
            <text class="card-text">全屏预览</text>
          </view>
          <view class="cardname">
            <text class="card-name">{{item.name}}</text>
          </view>
          <view class="cardvip">
            <text class="card-vip">会员免费</text>
          </view>
      </view>
  </view>
</template>

<script>
const app = getApp()
export default {
    data() {
      return {
        cardlist: [
          {
            name: '商务模板A',
            img: app.globalData.imageUrl + 'a.jpg',
            httpimg: 'https://cms.ednet.cn/UserFiles/teste/Images/%E5%B0%8F%E7%A8%8B%E5%BA%8F%EF%BC%88%E5%88%AB%E5%88%A0%EF%BC%89/al.jpg'

          },
          {
            name: '商务模板B',
            img: app.globalData.imageUrl + 'b.jpg',
            httpimg: 'https://cms.ednet.cn/UserFiles/teste/Images/%E5%B0%8F%E7%A8%8B%E5%BA%8F%EF%BC%88%E5%88%AB%E5%88%A0%EF%BC%89/bl.jpg'

          },
          {
            name: '商务模板C',
            img: app.globalData.imageUrl + 'c.jpg',
            httpimg: 'https://cms.ednet.cn/UserFiles/teste/Images/%E5%B0%8F%E7%A8%8B%E5%BA%8F%EF%BC%88%E5%88%AB%E5%88%A0%EF%BC%89/clp.png'

          },
          {
            name: '商务模板D',
            img: app.globalData.imageUrl + 'd.jpg',
            httpimg: 'https://cms.ednet.cn/UserFiles/teste/Images/%E5%B0%8F%E7%A8%8B%E5%BA%8F%EF%BC%88%E5%88%AB%E5%88%A0%EF%BC%89/dlp.png'

          }
        ]
      }
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
      }
    }
}
</script>

<style>

</style>
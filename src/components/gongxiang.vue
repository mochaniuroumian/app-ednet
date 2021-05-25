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
export default {
    data() {
      return {
        cardlist: [
          {
            name: '商务模板A',
            img: '/static/al.jpg',
            httpimg: 'https://cms.ednet.cn/UserFiles/teste/Images/%E6%A8%A1%E6%9D%BF/al.jpg'

          },
          {
            name: '商务模板B',
            img: '/static/bl.jpg',
            httpimg: 'https://cms.ednet.cn/UserFiles/teste/Images/%E6%A8%A1%E6%9D%BF/bl.jpg'

          },
          {
            name: '商务模板C',
            img: '/static/bl.jpg',
            httpimg: 'https://cms.ednet.cn/UserFiles/teste/Images/%E6%A8%A1%E6%9D%BF/bl.jpg'

          },
          {
            name: '商务模板D',
            img: '/static/bl.jpg',
            httpimg: 'https://cms.ednet.cn/UserFiles/teste/Images/%E6%A8%A1%E6%9D%BF/bl.jpg'

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
<template>
  <view class="container cardinfo">
    <view class="cardinfo-con">
      <view class="logo"><image mode="aspectFit" :src="imageUrl"></image></view>
	  <view class="colorwhite bigfont ede">e德互联</view>
      <view class="wearegold"><text class="wearegold-text">我们是金牌网络服务商</text></view>
      <view class="sixteen">
          <text class="sixteen-text">16</text>
          <text class="sixteen-year">年客户选择</text>
      </view>
      <view class="havebeen">
          <text class="we-text">我们</text>
          <text class="havebeen-year">一直在</text>
          <text class="tryhard">努力</text>
      </view>
      <view class="become"><text class="become-text">成为</text></view>
      <view class="networkservice"><button class="network-text" open-type="contact">您的网络服务商</button></view>
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
            choose: {
                chooseCard: 1,
                choosePhone: 0,
                addColor: "none",
                disabled: true
            },
            imageUrl:app.globalData.imageUrl + "logo.png",
            imageUrlback:app.globalData.imageUrl + "background.jpg"
        }
    },
    components: {
        footer
    }
}
</script>
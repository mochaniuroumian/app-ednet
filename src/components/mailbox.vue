<template>
  <view class="mailbox">
      <view class="ali"><text class="ali-text">阿里企业邮箱</text></view>
      <view class="alichoose"><text class="alich-text">安全&amp;稳定之选&nbsp;百万企业信任之选</text></view>
      <view class="aite"><image mode="aspectFit" :src="imageUrlaite"></image></view>
      <view class="edeali"><text class="edeali-text">e德互联15年阿里云企业邮箱金牌代理商</text></view>
      <view class="goldservice"><view class="gold-text">金牌服务</view></view>
      <view class="afterservice"><view class="after-text">无忧售后</view></view>
      <view class="vipservice"><view class="vipservice-text">1V1专属客服</view></view>
      <view class="customerservice"><button class="customer-text" open-type="contact">免费咨询</button></view>
      <view class="customerimg"><image mode="aspectFill" :src="imageUrlsmall"></image></view>
  </view>
</template>

<script>
const app = getApp()
export default {
    data() {
        return {
            imageUrlaite:app.globalData.imageUrl + "aite.png",
            imageUrlsmall:app.globalData.imageUrl + "smallgirl.png"
        }
    }
}
</script>

<style>

</style>
<template>
  <view class="vhost">
      <view class="windowsimg"><image mode="aspectFit" :src="windows"></image></view>
      <view class="winvhost"><text class="vhost-text">windows虚拟主机</text></view>
      <view class="oldbetter"><text class="old-text">更加适合老旧网站运行</text></view>
      <view class="type">
        <view class="type-text">基础</view>
        <view class="type-text">标准</view>
        <view class="type-text">企业</view>
      </view>
      <view class="linuximg"><image mode="aspectFit" :src="ubuntu"></image></view>
      <view class="linux"><text class="linux-text">Linux云主机</text></view>
      <view class="front"><text class="front-text">适合现代前端技术</text></view>
      <view class="tool">
        <view class="caddy">
          <image mode="aspectFit" :src="caddy"></image>
          <image mode="heightFix" :src="caddy2"></image>
        </view>
        <view class="docker">
          <image mode="heightFix" :src="docker"></image>
        </view>
      </view>
  </view>
</template>

<script>
const app = getApp()
export default {
    data() {
        return {
            windows:app.globalData.imageUrl + "windows.png",
            ubuntu:app.globalData.imageUrl + "ubuntu.png",
            caddy:app.globalData.imageUrl + "caddy.png",
            caddy2:app.globalData.imageUrl + "caddy2.png",
            docker:app.globalData.imageUrl + "docker.png",
        }
    }
}
</script>

<style>

</style>
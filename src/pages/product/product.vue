<template>
    <view class="container product">
      <view class="hello">
          <view class="user">欢迎您，{{uname}}</view>
          <view class="user-img"><image mode="aspectFit" :src="uimg"></image></view>
      </view>
      <image class="background" mode="aspectFill" src="/static/background.jpg"></image>
    </view>
</template>
<script>
export default {
    data() {
        return {
            uname: '',
			uimg: ''
        }
    },
    onLoad(options) {
        this.uname = options.name
        this.uimg = options.img
    },
}
</script>
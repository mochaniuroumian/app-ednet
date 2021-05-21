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
          <view class="content">
            <view v-show="product === 0">
                选项卡1的内容
            </view>
            <view v-show="product === 1">
                选项卡2的内容
            </view>
            <view v-show="product === 2">
                选项卡3的内容
            </view>
          </view>
      </view>

      <!-- <view class="tabbar">
          <uni-segmented-control :current="current" :values="items" @clickItem="onClickItem" 
              styleType="button" activeColor="#a9d682"></uni-segmented-control>
      </view> -->
      <image class="background" mode="aspectFill" src="/static/background.jpg"></image>
    </view>
</template>
<script>
import {uniSegmentedControl} from '@dcloudio/uni-ui'
export default {
    data() {
        return {
            uname: '未登录用户',
			uimg: '/static/logo.png',
            current:0,
            product:0,
            items:['','+',''],
            productItems:['共享建站','域名申请','企业邮箱','虚拟主机','微信小程序']
        }
    },
    created() {
        uni.$on('update',(data)=>{
          console.log('监听到时间来自update,携带参数msg为:' + data.uname)
        })
    },
    methods: {
        productItem(res){
          this.product=res.currentIndex;
        },
        onClickItem(res){
          this.current=res.currentIndex;
        }
    },
    components: {uniSegmentedControl}
}
</script>
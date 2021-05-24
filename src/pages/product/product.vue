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
          <view class="pro-content">
            <Gongxiang v-if="product === 0">
            </Gongxiang>
            <view v-if="product === 1">
                选项卡2的内容
            </view>
            <view v-if="product === 2">
                选项卡3的内容
            </view>
          </view>
      </view>
      <Footer></Footer>
      <image class="background" mode="aspectFill" src="/static/background.jpg"></image>
    </view>
</template>
<script>
import {uniSegmentedControl} from '@dcloudio/uni-ui'
import gongxiang from '../../components/gongxiang'
import footer from '../../components/footer'
export default {
    data() {
        return {
            uname: '未登录用户',
			uimg: '/static/logo.png',
            current:0,
            product:0,
            productItems:['共享建站','域名申请','企业邮箱','虚拟主机','微信小程序']
        }
    },
    onLoad(options) {
        this.uname = options.name,
        this.uimg = options.img
    },
    components: {
        uniSegmentedControl,
        gongxiang,
        footer
    },
    methods: {
        productItem(res){
          this.product=res.currentIndex;
        },
        onClickItem(res){
          this.current=res.currentIndex;
        }
    }
}
</script>
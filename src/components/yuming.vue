<template>
  <view class="yuming">
      <view class="yulike"><text class="yu-like">选择您喜欢的域名后缀</text></view>
      <view class="yucard">
          <uni-segmented-control :current="yunumber" :values="yuItems" @clickItem="yuItem" 
              styleType="button" activeColor="#007aff"></uni-segmented-control>
            <view class="yucard-content">
              <view v-show="yunumber === index" v-for="(item, index) in yucard" :key="index">
                  <view class="yucard-name">
                      <text class="name-text">{{item.name}}</text>
                  </view>
                  <view class="yucard-des">
                      <text class="des-text">{{item.des}}</text>
                  </view>
                  <view class="yucard-price">
                      <text class="price-text">{{item.price}}</text>
                      <text class="price-year">元/年</text>
                      <text class="price-go">起</text>
                  </view>
              </view>
            </view>
      </view>
  </view>
</template>

<script>
import {uniSegmentedControl} from '@dcloudio/uni-ui'
export default {
    data() {
        return {
          yunumber: 0,
          yuItems: ['.COM', '.CN', '.ORG'],
          yucard: [
              {
                  name: '国际顶级域名',
                  des: '',
                  price: '58'
              },
              {
                  name: '国内顶级域名',
                  des: '',
                  price: '58'
              },
              {
                  name: '国内顶级域名',
                  des: '',
                  price: '38'
              }
          ]
        }
    },
    components: {
        uniSegmentedControl
    },
    methods: {
        yuItem(res){
          this.yunumber=res.currentIndex;
        }
    }
}
</script>

<style>

</style>
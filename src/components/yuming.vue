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
          yuItems: ['.COM', '.CN', '.CO'],
          yucard: [
              {
                  name: '国际顶级域名',
                  des: '为company/commerce等等的简称，表示公司、企业、商业、贸易等等。在国际上用于广泛的知名度和应用，很多公司都选择.com域名进行网站宣传。',
                  price: '150'
              },
              {
                  name: '国内顶级域名',
                  des: '中国国家顶级域名，属于国家或地区顶级域名(ccTLD)，CN代表中国。有利于维护国家互联网信息安全；适用中国法律，'+
                  '全面保障用户利益；全中文服务，保障用户知情权；可注册域名资源丰富；显著的标识作用，体现自身的价值和定位。',
                  price: '100'
              },
              {
                  name: '商业公司的缩写',
                  des: '英文“Corporation、Company”（商业公司）的缩写，且仅2个字母，含义明确、简单易记，方便公众理解。极具竞争力的域名。',
                  price: '220'
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
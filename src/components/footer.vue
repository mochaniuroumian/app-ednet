<template>
  <view class="footer">
      <view class="cardinfos">
        <button plain="true" @click="cardinfo">
          <image v-if="choose.chooseCard === 0" mode="aspectFit" :src="cardinfoUrl"></image>
          <image v-if="choose.chooseCard === 1" mode="aspectFit" :src="cardchoose"></image>
        </button>
      </view>
      <view class="nav" :style="'background:' + choose.addColor">
        <button plain="true" @click="nav" :disabled="choose.disabled">
            <image mode="aspectFit" :src="jia"></image>
        </button>
        <uni-drawer ref="showRight" mode="right" width="100%" @change="drawerchange">
          <view class="navul">
            <view class="navlist" v-for="(item, index) in navlist" :key="index">
              <image mode="aspectFit" :src="item.imageUrl" @click="closeDrawer(item.productId)"></image>
              <view class="navname">{{item.navname}}</view>
            </view>
          </view>
        </uni-drawer>
      </view>
      <view class="contacts">
        <button plain="true" @click="contact">
          <image v-if="choose.choosePhone === 0" mode="aspectFit" :src="contactUrl"></image>
          <image v-if="choose.choosePhone === 1" mode="aspectFit" :src="contactchoose"></image>
        </button>
      </view>
  </view>
</template>

<script>
import {uniDrawer} from '@dcloudio/uni-ui'
const app = getApp()
export default {
    data() {
      return {
        cardinfoUrl: app.globalData.imageUrl + "cardinfo.png",
        cardchoose: app.globalData.imageUrl + "cardchoose.png",
        jia: app.globalData.imageUrl + "jia.png",
        contactUrl: app.globalData.imageUrl + "contact.png",
        contactchoose: app.globalData.imageUrl + "contactchoose.png",
        navlist: [
          {
            imageUrl: app.globalData.imageUrl + "yuming.png",
            navname: "域名",
            productId: 1
          },
          {
            imageUrl: app.globalData.imageUrl + "youxiang.png",
            navname: "邮箱",
            productId: 2
          },
          {
            imageUrl: app.globalData.imageUrl + "xuji.png",
            navname: "虚拟主机",
            productId: 3
          },
          {
            imageUrl: app.globalData.imageUrl + "app.png",
            navname: "App",
            productId: 0
          },
          {
            imageUrl: app.globalData.imageUrl + "gongxiang.png",
            navname: "共享建站",
            productId: 0
          },
          {
            imageUrl: app.globalData.imageUrl + "zhuomian.png",
            navname: "桌面开发",
            productId: 0
          },
          {
            imageUrl: app.globalData.imageUrl + "Group 25.png",
            navname: "微信小程序",
            productId: 4
          },
          {
            imageUrl: app.globalData.imageUrl + "gongzhong.png",
            navname: "微信公众号",
            productId: 0
          }
        ],
        drawerTag: false
      }
    },
    props: {
      choose: {
        type: Object
      }
    },
    components: {
      uniDrawer
    },
    methods: {
      cardinfo() {
        if(this.choose.chooseCard === 0){
          uni.navigateTo({
            url: '/pages/cardinfo/cardinfo'
          })
        }
      },
      drawerchange(res) {
          this.drawerTag = res
      },
      nav() {
        if(this.drawerTag) {
            this.$refs.showRight.close();
        }else {
            this.$refs.showRight.open();
        }
      },
      closeDrawer(index) {
        this.$emit('bottomPro', index)
        this.$refs.showRight.close();
      },
      contact() {
        if(this.choose.choosePhone === 0){
          uni.navigateTo({
            url: '/pages/contact/contact'
          })
        }
      }
    }
}
</script>
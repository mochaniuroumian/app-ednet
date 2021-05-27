<template>
  <view class="footer">
      <view class="cardinfos">
        <button plain="true" @click="cardinfo">
          <image v-if="choose.chooseCard === 0" mode="aspectFit" src="/static/cardinfo.png"></image>
          <image v-if="choose.chooseCard === 1" mode="aspectFit" src="/static/cardchoose.png"></image>
        </button>
      </view>
      <view class="nav" :style="'background:' + choose.addColor">
        <button plain="true" @click="nav">
          <image mode="aspectFit" src="/static/jia.png"></image>
        </button>
      </view>
      <view class="contacts">
        <button plain="true" @click="contact">
          <image v-if="choose.choosePhone === 0" mode="aspectFit" src="/static/contact.png"></image>
          <image v-if="choose.choosePhone === 1" mode="aspectFit" src="/static/contactchoose.png"></image>
        </button>
      </view>
  </view>
</template>

<script>
export default {
    props: {
      choose: {
        type: Object
      }
    },
    methods: {
      cardinfo() {
        if(this.choose.chooseCard === 0){
          uni.navigateTo({
            url: '/pages/cardinfo/cardinfo'
          })
        }
      },
      nav() {

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
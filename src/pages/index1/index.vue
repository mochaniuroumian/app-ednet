<template>
  <view class="container">
  <view class="card_wrap">
    <view @click="slidethis" :animation="id === 0 ? animationData : ''" :class="['card_item', 'card'+ (id + 1)]" v-for="(item, id) in cardInfoList" 
     :key="id" :style="'z-index: '+ (cardInfoList.length - id) +';transform: translateY('+ (32 - 6*id) + 'px) translateX(' + (20 + 6*id) +'px);'">
      <span class="change_icon" @tap="slidethis" v-if="id === 0">
        <image src="../../static/changeicon.png"></image>
      </span>
      <image mode="aspectFill" :src="item.cardUrl"></image>
    </view>
  </view>
</view>

</template>

<script>
const app = getApp();
export default {
    data() {
        return {
            animationData: {},
    cardInfoList: [{
      cardUrl: '../../static/moreposter1.jpg',
      cardInfo: {
        cardTitle: '',
        cardInfoMes: []
      }
    }, {
      cardUrl: '../../static/moreposter2.jpg',
      cardInfo: {
        cardTitle: '',
        cardInfoMes: []
      }
    },{
      cardUrl: '../../static/moreposter3.jpg',
      cardInfo: {
        cardTitle: '',
        cardInfoMes: []
      }
    }
  ]
        }
    },
    onLoad: function () {
    // 调用应用实例的方法获取全局数据
    app.getUserInfo(userInfo => {
      //更新数据
        this.userInfo=userInfo
    })
  },
  methods: {
      slidethis: function(e) {
    var animation = uni.createAnimation({
      duration: 700,
      timingFunction: 'cubic-bezier(.8,.2,.1,0.8)',
    });
    var that = this;
    this.animation= animation;
    this.animation.translateY(-520).rotate(-5).translateX(0).step();
    this.animation.translateY(32).translateX(20).rotate(0).step();
      this.animationData= this.animation.export();
    var cardInfoLists, slidethis
    setTimeout(function() {
      cardInfoLists = this.cardInfoList;
      var slidethis2 = that.cardInfoList.slice(1,2);
      slidethis = that.cardInfoList.shift();
      that.cardInfoList.unshift(slidethis2[0]);
        this.cardInfoList= this.cardInfoList,
        this.animationData= {}
    }, 500);
    setTimeout(function() {
      that.cardInfoList.splice(1,1);
      that.cardInfoList.push(slidethis);
        cardInfoLists = that.cardInfoList,
        this.animationData= {}
    }, 1500);
  },
  }
}
</script>

<style lang="scss" scoped>
.card_wrap {
  background: #f2f2f6;
  position: relative;
  width: 100%;
  height: 100%;
}
.card_wrap .card_item {
  position: absolute;
  width: 85%;
  height: 90%;
}
.card_wrap .card_item span.change_icon image {
  position: absolute;
  width: 35px;
  height: 11px;
  top: 14px;
  left: 50%;
  margin-left: -17px;
  box-shadow:none;
}
.card_wrap .card_item image {
  display: block;
  width: 100%;
  height: 100%;
  border-radius: 6px;
  box-shadow: 6px 23px 50px 10px #ccc;
}

</style>
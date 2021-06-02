<template>
  <view class="container">
  <view class="card_wrap">
    <view class="card_item">
      <span class="change_icon" bindtouchend="listenerButtonPlay">
        <image :class="['icon1', auto?'':'auto']" src="../../static/yinyue.png" @tap="autoMusic"></image>
      </span>
      <span class="change_icon">
        <image class="icon2" src="../../static/dianhua.png" @click='freeTell'></image>
      </span>
      <span class="change_icon">
        <button open-type="contact">
        <image class="icon3" src="../../static/kefu.png"></image>
      </button>
      </span>
      <button class="more" plain="true" @tap="openapp">服务详情 >></button>
      <image mode="aspectFill" show-menu-by-longpress bindlongpress="longPressSaveImg " src="../../static/image-ednet2.jpg"></image>
    </view>
  </view>
</view>
</template>

<script>
var app = getApp();
const bgMusic = uni.getBackgroundAudioManager() 
export default {
    data() {
        return {
            musictitle:'e德互联',
            phone:'4006511688',
            auto: false,
            mp3url: app.globalData.imageUrl + 'gangqin16s.wav'
        }
    },
    onLoad: function () {
    this.listenerButtonPlay()
    uni.showShareMenu({
      withShareTicket:true,
      menus:["shareAppMessage","shareTimeline"]
      })
    },
    methods: {
        listenerButtonPlay: function () {
    　　var that = this
    　　var src = this.mp3url
    　　bgMusic.title = this.musictitle;
    　　bgMusic.src = src;　　//自动播放
    　　bgMusic.onTimeUpdate(() => { //监听音频播放进度
    　　　　//console.log(bgMusic.currentTime)
    　　})
    　　bgMusic.onEnded(() => { //监听音乐自然播放结束
    　　　　that.listenerButtonPlay(src)    //r如果需要音乐结束后继续循环播放，解除注释
    　　})
    　　bgMusic.pause(); //播放音乐
    },
    //停止播放
    listenerButtonStop: function () {
    　　bgMusic.stop()
    },
     
    autoMusic: function (e) {
    　　var that = this;
    　　　　this.auto= !this.auto
    　　if (this.auto) {
      　　　　bgMusic.pause();
    　　} else {
           bgMusic.title = this.musictitle 
    　　　　bgMusic.src = this.mp3url
    　　　　bgMusic.play();
    　　}
    },
    freeTell: function(){
      uni.makePhoneCall({
        phoneNumber: this.phone,
      })
    },
    //20200720 新增长按保存图片
  longPressSaveImg (e) {
    let that = this
    let url = e.currentTarget.dataset.url;
    console.log(url);
    if (!uni.saveImageToPhotosAlbum) {
      uni.showModal({
        title: '提示',
        content: '当前微信版本过低，无法使用该功能，请升级到最新微信版本后重试。'
      })
      return;
    }
    // 检查用户授权
    uni.getSetting({
      success(res) {
        if (!res.authSetting['scope.writePhotosAlbum']) {
          // 接口调用询问  
          uni.authorize({
            scope: 'scope.writePhotosAlbum',
            success() {
              that.saveImg(url);
            },
            fail() {
              // 用户拒绝授权  
              uni.showModal({
                title: '保存图片',
                content: '保存图片需要您授权',
                showCancel: true,
                confirmText: '确定',
                success (res) {
                  if (res.confirm) {
                    // 打开设置页面  
                    uni.openSetting({
                      success (res) {
                        if (res.authSetting['scope.writePhotosAlbum']) {
                          that.saveImg(url);
                        } else {
                          uni.showToast({
                            title:'授权失败!',
                            icon:"none"
                           });
                        }
                      },
                      fail (res) {
                        uni.showToast({
                          title:'授权失败!',
                          icon:"none"
                         });
                      }
                    });
                  } else if (res.cancel) {
                    uni.showToast({
                      title:'您已取消授权!',
                      icon:"none"
                     });
                  }
                }
              })
            }
          })
        } else {
          that.saveImg(url)
        }
      },
      fail(res) {
        console.log(res);
      }
    })
  },
  saveImg (imageUrl) { 
     uni.getImageInfo({
         src: imageUrl,
         success:(res)=> {
          let path = res.path;
            uni.saveImageToPhotosAlbum({
             filePath:path,
             success:(res)=> { 
                uni.showToast({
                title:'保存成功'
                });
             },
             fail:(res)=>{
                uni.showToast({
                  title:'您已取消保存',
                  icon:"none"
                });
             }
            })
           },
         fail:(res)=> {
          console.log(res);
        }
    })
  },
  openapp (){
    uni.navigateTo({
      url: '../../pages/index1/index'
    })
    this.autoMusic ()
  },
  //发送给朋友
  onShareAppMessage(res) {
  // 此处的distSource为分享者的部分信息，需要传递给其他人
  let distSource = uni.getStorageSync('distSource');
  if (distSource) {
  return {
  title: 'e德互联欢迎你',
  type: 0,
  path: '/pages/indexmusic/index',
  summary: "",
  imageUrl: "这个是分享图片地址"
  }
  }
  },
  //分享到朋友圈
  onShareTimeline(res) {
  let distSource = uni.getStorageSync('distSource');
  if (distSource) {
  return {
  title: 'e德互联欢迎你',
  type: 0,
  query: 'id=' + distSource, //这个是参数
  summary: "",
  imageUrl: "这个是分享图片地址"
  }
  }
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
  width: 100%;
  height: 100%;
}
.card_wrap .card_item .change_icon>image,.card_wrap .card_item .change_icon button {
  position: absolute;
  padding:8px;
  width: 20px;
  height: 20px;
  right: 10px;
  box-shadow:#ccc 0 0 10px;
  background-color: #fffc;
  border-radius: 50%;
}
.card_wrap .card_item .change_icon button {
  bottom: 100px;
  width: 36px;
  height: 36px;
}
.card_wrap .card_item .change_icon .icon1 {
  top: 10px;
}
.card_wrap .card_item .change_icon .icon2 {
  bottom: 150px;
}
.card_wrap .card_item .change_icon .icon3 {
  width: 100%;
  height: 100%;
  position: initial;
}
@-webkit-keyframes rotation{
  from {-webkit-transform: rotate(0deg);}
  to {-webkit-transform: rotate(360deg);}
  }
.card_wrap .card_item .change_icon .auto{
  -webkit-transform: rotate(360deg);
  animation: rotation 3s linear infinite;
  -moz-animation: rotation 3s linear infinite;
  -webkit-animation: rotation 3s linear infinite;
  -o-animation: rotation 3s linear infinite;
  }
.card_wrap .card_item .more {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  bottom: 20%;
  /* width: 100px; */
  border-radius: 30px;
  border: 1px #e98f36 solid;
  color:#e98f36;
  line-height: 18px;
  padding: 14rpx 56rpx;
  }
.card_wrap .card_item image {
  display: block;
  width: 100%;
  height: 100%;
}
</style>
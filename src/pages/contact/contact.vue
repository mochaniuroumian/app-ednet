<template>
    <view class="container contact">
      <view class="contact-con">
        <view class="map">
          <map :latitude="latitude" :longitude="longitude" :markers="covers"></map>
        </view>
        <view class="contactinfo">
            <view class="erweima"><image mode="aspectFit" src="/static/erweima.jpg"></image></view>
            <view class="infos" v-for="(item, index) in infos" :key="index">
                <image mode="aspectFit" :src="item.icon"></image>
                <view class="name">{{item.name}}</view>
                <view class="name-text">{{item.nametext}}</view>
            </view>
        </view>
      </view>
      <Footer :choose = choose></Footer>
      <image class="background" mode="aspectFill" src="/static/background.jpg"></image>
  </view>
</template>

<script>
import footer from '@/components/footer'
export default {
    data() {
        return {
            latitude: 39.120615,
            longitude: 117.180686,
            covers: [{
                id:0,
                latitude: 39.120615,
                longitude: 117.180686,
                iconPath: '/static/lucky.png'
            }],
            choose: {
                chooseCard: 0,
                choosePhone: 1,
                addColor: "none"
            },
            infos: [
                {
                    icon: "/static/gps.png",
                    name: "公司名称：",
                    nametext: "天津市德林瑞泰科技开发有限公司天津市德林瑞泰科技开发有限公司"
                },
                {
                    icon: "/static/site.png",
                    name: "地址：",
                    nametext: "天津市德林瑞泰科技开发有限公司"
                },
                {
                    icon: "/static/phone.png",
                    name: "电话：",
                    nametext: "天津市德林瑞泰科技开发有限公司"
                },
                {
                    icon: "/static/mail.png",
                    name: "邮箱：",
                    nametext: "天津市德林瑞泰科技开发有限公司天津市德林瑞泰科技开发有限公司"
                }
            ]
        }
    },
    components: {
        footer
    }
}
</script>
<script>
	export default {
		onLaunch: function() {
			//调用API从本地缓存中获取数据
            var logs = uni.getStorageSync('logs') || []
            logs.unshift(Date.now())
            uni.setStorageSync('logs', logs)
            // uni.cloud.init({
            //   env:'cloud1-5gxfdiwq5014011e'
            // })
		},
		onShow: function() {
		},
		onHide: function() {
		},
		getUserInfo:function(cb){
            var that = this
            if(this.globalData.userInfo){
              typeof cb == "function" && cb(this.globalData.userInfo)
            }else{
            //调用登录接口
              uni.login({
                success () {
                  uni.getUserInfo({
                    success: function (res) {
                      that.globalData.userInfo = res.userInfo
                      typeof cb == "function" && cb(that.globalData.userInfo)
                    }
                  })
                }
              })
            }
        },
		globalData: {
			imageUrl: "https://tempc.51comm.cn/imgs/ednet/",
			userInfo:null
		}
	}
</script>

<style lang='scss'>
    @import "pages/css/index.scss";
	/*每个页面公共css */
</style>

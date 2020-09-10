<template>
  <div class="app">
    <div class="mod">
      <img src="../../../dist/wx/static/images/0.jpg" alt="">
      <p>武汉的马路恢复了喧嚣</p>
      <p>武汉的早餐摊重又熙熙攘攘</p>
    </div>
     <div class="box">
       <img @tap="toDetail" v-if='isShow' :src="userinfo.avatarUrl" />
       <button class="but" v-else open-type="getUserInfo" @getuserinfo="getUserInfo">加入</button>
     </div>
  </div>
</template>

<script>
  export default{
    data () {
      return {
        userinfo: {},
        isShow: false
      }
    },
    beforeMount () {
      // 获取用户登录信息
      this.handleGetUserInfo()
    },
    methods: {
      // 获取用户登录信息
      handleGetUserInfo () {
        wx.getUserInfo({
          success: (data) => {
            this.userinfo = data.userInfo
            // console.log(data)
            // console.log('用户头像' + this.userinfo.avatarUrl)
            // console.log('用户名' + this.userinfo.nickName)
            this.isShow = true
          },
          fail: () => {
            console.log('获取失败')
          }
        })
      },

      getUserInfo (data) {
        // 判断用户是否授权
        console.log(data)
        if (data.mp.detail.rawData) {
          this.handleGetUserInfo()
        }
      },
      toDetail () {
        wx.navigateTo({
          url: '/pages/list/main'
        })
      }
    }
  }
</script>

<style>
  .mod{
    position: relative;
    width: 100%;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .mod{
    position: relative;
    width: 100%;
    overflow-y: auto;
  }
  .mod img{
    width: 100%;
    height: 5rem;
    margin-bottom: 60rpx;
  }
  .mod p{
    height: 50rpx;
    line-height: 50rpx;
    text-align: center;
  }
  .box{
    position: absolute;
    width: 100%;
    overflow-y: auto;
    padding-top: 60rpx;
    box-sizing: border-box;
    bottom: 150rpx;
  }
  .box p,.but{
    width: 150rpx;
    height: 150rpx;
    border: 1rpx solid #eee;
    line-height: 150rpx;
    text-align: center;
    margin: 0 auto;
    border-radius: 50%;
    font-size: 40rpx
  }
  .but{
    background-color: #f0f0f0;
  }
  .box img{
    position: relative;
    width: 150rpx;
    height: 150rpx;
    margin: 0 auto;
    border-radius: 50%;
    left: 50%;
    margin-left: -75rpx;
  }
</style>

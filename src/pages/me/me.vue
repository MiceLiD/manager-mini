<template>
<div class="user-profile">
  <div class="user-info">
    <div class="info" v-if="userInfo.avatarUrl">
      <img :src="userInfo.avatarUrl"></img>
      <span>{{userInfo.nickName}}</span>
    </div>
    <div class="extra" v-if="userInfo.avatarUrl">
      <div class="extra-item">
        <div class="label">
          性别：
        </div>
        <div class="value">
          {{ userInfo.extra.gender }}
        </div>
      </div>
      <div class="extra-item">
        <div class="label">
          地区：
        </div>
        <div class="value">
          {{ userInfo.extra.location }}
        </div>
      </div>
    </div>
  </div>
  <button 
    @getuserinfo="bindAction" 
    open-type='getUserInfo' 
    class="btn-login" 
    hover-class="gray" 
    :type="bType" >{{ actionText }}</button>
</div>
</template>

<script>

export default {
  data () {
    return {
      userInfo: {
        avatarUrl: "",
        nickName: "未登录"
      },
      bType: "primary", // 按钮类型
      actionText: "登录", // 按钮文字提示
      lock: false //登录按钮状态，false表示未登录
    }
  },
  onLoad() {
    wx.getStorage({
      key: 'userInfo',
      success: (res) => {
        wx.hideLoading()
        this.userInfo = {
          avatarUrl: res.data.userInfo.avatarUrl,
          nickName: res.data.userInfo.nickName,
          extra: res.data.userInfo.extra
        }
        this.bType = res.data.bType
        this.actionText = res.data.actionText
        this.lock = true
      }
    })
  },

  methods: {
    bindAction: function (e) {
      const { detail } = e.mp
      const { rawData } = detail
      const userInfo = JSON.parse(rawData)
      const { nickName, gender, city, province, country, avatarUrl } = userInfo
      this.lock = !this.lock
      if (this.lock) {
        this.userInfo = {
          avatarUrl,
          nickName,
          extra: {
            gender: gender === 1 ? 'boy' : 'girl',
            location: `${country} ${province} ${city}`
          }
        }
        this.bType = "warn",
        this.actionText = "退出登录"
        wx.setStorage({
          key: 'userInfo',
          data: {
            userInfo: {
              avatarUrl,
              nickName,
              extra: {
                gender: gender === 1 ? 'boy' : 'girl',
                location: `${country} ${province} ${city}`
              }
            },
            bType: "warn",
            actionText: "退出登录"
          },
          success: function (res) {
            console.log("存储成功")
          }
        })
        // 如果已经登录，退出登录按钮操作     
      } else {
        wx.showModal({
          title: "确认退出?",
          content: "真是个狼灭，😕",
          success: (res) => {
            if (res.confirm) {
              wx.removeStorageSync('userInfo')
              this.userInfo = {
                avatarUrl: "",
                nickName: "未登录"
              }
              this.bType = "primary",
              this.actionText = "登录"
            } else {
              this.lock = true
            }
          }
        })
      }
    }
  },

  created () {
    // let app = getApp()
  }
}
</script>

<style scoped lang="less">
.user-profile {
  .user-info{
    background-color: #fff;
    .info {
      padding: 10px 20px;
      img{
        display: inline-block;
        width: 50px;
        height: 50px;
        border-radius: 50%;
        border: 1rpx solid rgba(0,0,0,.2);
        vertical-align: middle;
      }
      span{
        display: inline-block;
        margin-left: 20px;
      }
    }
    .extra {
      margin-top: 30px;
      border-top: 1rpx solid rgba(0,0,0,.2);
      .extra-item {
        padding: 10px 0;
        display: flex;
        align-items: center;
        justify-content: space-between;
        border-bottom: 1rpx solid rgba(0,0,0,.2);
        .label {
          width: 200rpx;
          padding-left: 20px;
        }
        .value {
          flex: 1;
        }
      }
    }
  }
  .btn-login{
    position: absolute;
    bottom: 60px;
    width: 90%;
    left: 50%;
    margin-left: -45%;
  }
  .gray{
    background-color: #ccc;
  }
}
</style>

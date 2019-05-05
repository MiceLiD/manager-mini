<template>
<div class="index">
  <swiper
    class='slide-image'
    indicator-dots='true'
    indicator-active-color='#ffffff'
    autoplay='true'>
    <div v-for="(url, index) in imgUrls" :key="index">
      <swiper-item>
        <div class='img-wrapper' :style="{
          width: '100%', 
          height: '100%',
          backgroundSize: '100%',
          backgroundRepeat: 'no-repeat',
          backgroundImage: 'url(' + url + ')'
        }"></div>
      </swiper-item>
    </div>
  </swiper>
  <div class='menu-wrapper'>
    <div v-for="(menu, index) in menus" :key="index">
      <div class='menu-item' @click="navigateTo($event, menu)">
        <div class='item-icon'>
          {{ index }}
        </div>
        <div class='item-text'>
          {{ menu.text }}
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>

export default {
  data () {
    return {
      imgUrls: Array(3).fill('').map((item, index) => `https://raw.githubusercontent.com/MiceLiD/manager-mini-images-cloud/master/images/image/swipe${index}.jpg`),
      menus: [
        {
          title: '注册公司',
          name: 'register-company'
        }, {
          title: '记账报税',
          name: 'bookkeep-tax'
        }, {
          title: '公司变更',
          name: 'change-company'
        }, /*{
          title: '社保开户',
          name: ''
        }, */{
          title: '对公账户',
          name: 'public-accounts'
        }, /*{
          title: '各类经营许可',
          name: ''
        }, {
          title: '代购发票',
          name: ''
        }, */{
          title: '注册商标',
          name: 'register-mark'
        }, /*{
          title: '申请专利',
          name: ''
        }, {
          title: '网站/小程序',
          name: ''
        }, */{
          title: '公司注销',
          name: 'logout-company'
        }, /*{
          title: '税务筹划',
          name: ''
        }*/
      ].map(item => {
        const { title, name } = item
        return {
          iconUrl: '',
          text: title,
          advidory: '',
          imgUrl: `https://raw.githubusercontent.com/MiceLiD/manager-mini-images-cloud/master/images/image/detail/${name}.jpg`
        }
      })
    }
  },

  methods: {
    navigateTo (e, item) {
      const { text, imgUrl, advidory } = item
      wx.navigateTo({
        url: `/pages/detail/main?text=${text}&imgUrl=${imgUrl}&advidory=${advidory}`
      })
    }
  },

  created () {
    let app = getApp()
  }
}
</script>

<style scoped lang="less">
.slide-image {
  width: 100%;
}
.menu-wrapper {
  background-color: #ffffff;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 20px 20px;
  padding: 20px;
  .menu-item {
    text-align: center;
    .item-icon {
      width: 50px;
      height: 50px;
      border: 1px solid #1296db;
      display: inline-block;
      border-radius: 30%;
      overflow: hidden;
      line-height: 50px;
      text-align: center;
    }
    .item-text {
      padding: 3px 0;
      font-size: 14px;
    }
  }
}
</style>

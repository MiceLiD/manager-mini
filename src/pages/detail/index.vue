<template>
  <div class="detail">
    <div v-if="pagePic" class="detail-pic" :style="{
      width: '100%',
      backgroundSize: '100%',
      backgroundRepeat: 'no-repeat',
      backgroundImage: 'url(' + pagePic + ')'
    }">
    </div>
    <div class="detail-content">
      <template v-if="pageDetail.title === '注册公司'">
        <RegisterCompany />
      </template>
      <template v-if="pageDetail.title === '记账报税'">
        <BookkeepTax />
      </template>
    </div>
    <div class="detail-btns">
      <button @click="handleOnAdvidory">在线咨询</button>
      <button @click="handleOnOrder">在线下单</button>
    </div>
  </div>
</template>

<script>
import RegisterCompany from '@/components/register-company.vue'
import BookkeepTax from '@/components/bookkeep-tax.vue'
export default {
  data () {
    return {
      pageType: '',
      pagePic: '',
      pageDetail: {
        title: '',
        advidory: '', // 咨询
        orderUrl: ''
      }
    }
  },
  methods: {
    handleOnAdvidory() {},
    handleOnOrder() {},
  },
  onLoad: function (options) {
    const { text, imgUrl, advidory } = this.$root.$mp.query
    wx.setNavigationBarTitle({
      title: text
    })
    this.pageType = text
    this.pagePic = imgUrl
    this.pageDetail = {
      title: text,
      advidory,
      orderUrl: `/order?type=${text}`
    }
  },
  components: {
    RegisterCompany,
    BookkeepTax
  }
}
</script>

<style scoped lang="less">
.detail {
  height: 100vh;
  background-color: #ffffff;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  .detail-pic {
    width: 100%;
    height: 133px;
  }
  .detail-content {
    border-top: 1rpx dashed rgba(0,0,0,.1);
    border-bottom: 1rpx dashed rgba(0,0,0,.1);
    flex: 1;
    overflow: scroll;
  }
  .detail-btns {
    padding: 15px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    button {
      width: 45%;
      overflow: unset;
    }
  }
}
</style>

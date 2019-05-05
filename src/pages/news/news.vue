<template>
  <div class="news-list">
    <block v-for="(n, i) in newsList" :key="i">
      <div class='news-item-wrapper' @click="handleOnNewsItem($event, n.id)">
        <div class='news-item'>
          {{ n.title }}
        </div>
      </div>
    </block>
  </div>
</template>

<script>

export default {
  data () {
    return {
      newsList: []
    }
  },

  onLoad() {
    wx.request({
      url: 'https://www.easy-mock.com/mock/5ccbe84259548f2854decbab/company-creative/news-list',
      data: {},
      method: 'GET', // OPTIONS, GET, HEAD, POST, PUT, DELETE, TRACE, CONNECT
      // header: {}, // 设置请求的 header
      success: (res) => {
        this.newsList = res.data.data.list
      },
      fail: function(res) {
        // fail
      },
      complete: function(res) {
        // complete
      }
    })
  },

  methods: {
    handleOnNewsItem(e, id) {
      wx.navigateTo({
        url: `/pages/article-detail/main?articleId=${id}`
      })
    }
  },

  created () {
    // let app = getApp()
  }
}
</script>

<style scoped lang="less">
.news-list {
  .news-item-wrapper {
    border-bottom: 1rpx solid rgba(0,0,0,.1);
    padding: 10px;
    margin: 0 0 10px 10px;
    .news-item {
      font-size: 14px;
      overflow: hidden;
      text-overflow: ellipsis;
    }
  }
}
</style>

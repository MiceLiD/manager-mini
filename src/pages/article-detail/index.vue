<template>
  <div class="article-detail">
    <div class="article-title">
      {{ articleTitle }}
    </div>
    <div class="article-content">
      {{ articleContent }}
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      articleTitle: '',
      articleContent: ''
    }
  },
  onLoad() {
    const { articleId } = this.$root.$mp.query
    wx.request({
      url: 'https://www.easy-mock.com/mock/5ccbe84259548f2854decbab/company-creative/news-list',
      data: {},
      method: 'GET', // OPTIONS, GET, HEAD, POST, PUT, DELETE, TRACE, CONNECT
      // header: {}, // 设置请求的 header
      success: (res) => {
        const newsList = res.data.data.list
        const article = newsList.filter(item => item.id == articleId)[0]
        this.articleTitle = article.title
        this.articleContent = article.content
      },
      fail: function(res) {
        // fail
      },
      complete: function(res) {
        // complete
      }
    })
  }
}
</script>

<style lang="less" scoped>
.article-detail {
  height: 100vh;
  text-align: center;
  background-color: #ffffff;
  .article-title {
    font-size: 16px;
    text-align: center;
    padding: 20px 0;
  }
  .article-content {
    padding: 10px;
    font-size: 14px;
    text-indent: 5px;
  }
}
</style>


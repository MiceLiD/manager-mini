<template>
  <div class="container">
    <div class="item-title">
      记账报税
    </div>
    <div class="item-category">
      <radio-group @change="handleOnChange">
        <div class="radio" v-for="(item, index) in items" :key="index">
          <div class="radio-value">
            {{ item.name }}
          </div>
          <div class="radio-radio">
            <radio :value="item.value" />
          </div>
        </div>
      </radio-group>
    </div>
    <div class="item-title">
      服务流程
    </div>
    <div class="item-detail">
      <div class="process">
        <p v-for="(p, i) in process" :key="i">
          {{ p }}
        </p>
      </div>
      <div class="desc">
        所需材料：{{ processData[curVal] }}
      </div>
    </div>
    <div class="item-image" :style="{
      width: '100%',
      backgroundSize: '100%',
      backgroundRepeat: 'no-repeat',
      backgroundImage: 'url(https://raw.githubusercontent.com/MiceLiD/manager-mini-images-cloud/master/images/image/promise.png)'
    }"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {name: '小规模纳税人1500/年', value: '1500'},
        {name: '一般纳税人1500/年', value: '1-1500'},
        {name: '小规模纳税人4000/5年', value: '5-4000'},
        {name: '一般纳税人15000/5年', value: '5-15000'}
      ],
      process: [
        '① 票据收取',
        '② 会计记账',
        '③ 精密审查',
        '④ 纳税申报'
      ],
      curVal: '1500',
      processData: {
        '1500': '小规模纳税人/年 材料',
        '1-1500': '一般纳税人/年 材料',
        '5-4000': '小规模纳税人/5年 材料',
        '5-15000': '一般纳税人15000/5年 材料',
      }
    }
  },
  methods: {
    handleOnChange(e) {
      const value = e.mp.detail.value
      this.curVal = value
    }
  }
}
</script>

<style lang="less" scoped>
.container {
  .item-title {
    border-bottom: 1rpx solid rgba(0,0,0,.1);
    padding: 10px 0 10rpx 20px;
  }
  .item-category {
    font-size: 14px;
    padding: 10rpx 20px;
    .radio {
      padding: 5rpx;
      display: flex;
      align-items: center;
      .radio-value, .radio-radio {
        width: 50%;
      }
      .radio-radio {
        text-align: right;
      }
    }
  }
  .item-detail {
    padding: 10rpx 20px;
    font-size: 14px;
    display: flex;
    align-items: top;
    .process {
      width: 50%;
      p {
        padding: 5rpx 0;
      }
    }
    .desc {
      width: 50%;
    }
  }
  .item-image {
    margin-top: 10px;
    border-top: 1rpx solid rgba(0,0,0,.04);
    height: 100px;
  }
}
</style>

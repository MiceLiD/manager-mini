<template>
  <div class="container">
    <div class="item-title">
      营业执照注册
    </div>
    <div class="item-category">
      <radio-group @change="handleOnChange">
        <div class="radio" v-for="(item, index) in items" :key="index">
          <div class="radio-value">
            {{ item.value }}
          </div>
          <div class="radio-radio">
            <radio :value="item.name" />
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
        {name: '个体工商户', value: '个体工商户'},
        {name: '有限公司', value: '有限公司'},
        {name: '股份公司', value: '股份公司'},
        {name: '分公司', value: '分公司'},
        {name: '其他', value: '其他'}
      ],
      process: [
        '① 在线下单',
        '② 客服对接',
        '③ 资料交接',
        '④ 提交材料',
        '⑤ 领证完工'
      ],
      curVal: '个体工商户',
      processData: {
        '个体工商户': '个体工商户',
        '有限公司': '有限公司',
        '股份公司': '股份公司',
        '分公司': '分公司',
        '其他': '其他'
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

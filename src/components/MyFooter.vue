<template>
  <!-- 底部 -->
  <div class="my-footer">
    <!-- 全选 -->
    <div class="custom-control custom-checkbox">
      <input
        type="checkbox"
        class="custom-control-input"
        id="footerCheck"
        v-model="isAll"
      />
      <label class="custom-control-label" for="footerCheck">全选</label>
    </div>
    <!-- 合计 -->
    <div>
      <span>合计:</span>
      <span class="price">¥ {{ allMoney }}</span>
    </div>
    <!-- 按钮 -->
    <button type="button" class="footer-btn btn btn-primary">
      结算 ({{ count }} )
    </button>
  </div>
</template>

<script>
export default {
  props: {
    goodslist: {
      type: Array,
      required: true
    }
  },
  computed: {
    isAll: {
      get() {
        return this.goodslist.every((item) => item.goods_state)
      },
      set(val) {
        this.goodslist.forEach((item) => (item.goods_state = val))
      }
    },
    count() {
      return this.goodslist.reduce(
        (pre, cur) => (cur.goods_state ? pre + cur.goods_count : pre),
        0
      )
    },
    allMoney() {
      return this.goodslist.reduce(
        (pre, cur) =>
          cur.goods_state ? pre + cur.goods_count * cur.goods_price : pre,
        0
      )
    }
  }
}
</script>

<style lang="less" scoped>
.my-footer {
  position: fixed;
  z-index: 2;
  bottom: 0;
  width: 100%;
  height: 50px;
  border-top: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 10px;
  background: #fff;

  .price {
    color: red;
    font-weight: bold;
    font-size: 15px;
  }
  .footer-btn {
    min-width: 80px;
    height: 30px;
    line-height: 30px;
    border-radius: 25px;
    padding: 0;
  }
}
</style>

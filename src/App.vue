<template>
  <div class="app">
    <MyHeader title="购物车案例" background="gold" />
    <MyGoods v-for="item in goodslist" :key="item.goods_id" :goods="item" />
    <MyFooter :goodslist="goodslist" />
  </div>
</template>

<script>
import MyHeader from '#/MyHeader.vue'
import MyGoods from '#/MyGoods.vue'
import MyFooter from '#/MyFooter.vue'
import axios from 'axios'
export default {
  components: {
    MyHeader,
    MyGoods,
    MyFooter
  },
  data() {
    return {
      goodslist: []
    }
  },
  created() {
    this.getList()
  },
  methods: {
    async getList() {
      const res = await axios({ url: '/api/cart' })
      this.goodslist = res.data.list
    }
  }
}
</script>

<style scoped>
.app {
  padding: 50px 0;
  max-height: 100vh;
  overflow: auto;
}
</style>

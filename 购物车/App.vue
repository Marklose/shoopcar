<template>
  <div class="app">
    <MyHeader title="购物车案例" background="pink" color="red" />
    <MyGoods v-for="item in goodslist" :key="item.goods_id" :goods="item" />
    <MyFooter :goodslist="goodslist" />
  </div>
</template>

<script>
import MyHeader from '#/MyHeader.vue'
import MyFooter from '#/MyFooter.vue'
import MyGoods from '#/MyGoods.vue'
import axios from 'axios'
export default {
  components: {
    MyHeader,
    MyFooter,
    MyGoods
  },
  data() {
    return {
      goodslist: []
    }
  },
  created() {
    this.getGoods()
  },
  methods: {
    async getGoods() {
      const res = await axios({ url: '/api/cart ' })
      // console.log(res.data.list)
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

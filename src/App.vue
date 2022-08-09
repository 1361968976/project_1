<template>
  <div class="app-container">
    <Header title="购物车案例">头部区域</Header>
    <Goods
      :title="item.goods_name"
      :status="item.goods_state"
      :img="item.goods_img"
      :singalPrice="item.goods_price"
      :id="item.id"
      :count="item.goods_count"
      v-for="item in list"
      :key="item.id"
      @stateChange="getNewState"
    ></Goods>
    <Footer
      :allState="fullState"
      :AllPrice="totalPrice"
      @isAllState="isgetAllState"
      :totalCount="totalCount"
    ></Footer>
  </div>
</template>

<script>
import Header from "./components/header/header.vue";
import axios from "axios";
import Goods from "./components/goods/goods.vue";
import Footer from "./components/Footer/Footer.vue";
import bus from "./components/eventBus.js";

export default {
  data() {
    return {
      list: [],
    };
  },
  components: {
    Header,
    Goods,
    Footer,
  },
  methods: {
    async getCarList() {
      const { data: res } = await axios.get("https://www.escook.cn/api/cart");
      console.log(res.list);
      if (res.status === 200) {
        this.list = res.list;
      }
    },
    getNewState(val) {
      console.log(val);
      this.list.some((item) => {
        if (item.id === val.id) {
          item.goods_state = val.value;
        }
      });
    },
    isgetAllState(val) {
      this.list.forEach((item) => {
        item.goods_state = val;
      });
    },
  },
  created() {
    this.getCarList();
    bus.$on("NewGoodsInfoAdd", (val) => {
      console.log(val);
      this.list.some((item) => {
        if (item.id === val.id) {
          item.goods_count = val.value;
        }
      });
    });
    bus.$on("NewGoodsInfoLess", (val) => {
      console.log(val);
      this.list.some((item) => {
        if (item.id === val.id) {
          item.goods_count = val.value;
        }
      });
    });
  },
  computed: {
    fullState() {
      return this.list.every((item) => item.goods_state === true);
    },
    // 已勾选商品的总价
    totalPrice() {
      return this.list
        .filter((item) => item.goods_state === true)
        .reduce(
          (total, item) => (total += item.goods_price * item.goods_count),
          0
        );
    },
    totalCount() {
     return this.list
        .filter((item) => item.goods_state)
        .reduce((t, item) => (t += item.goods_count), 0);
    },
  },
};
</script>

<style lang="less" scoped>
</style>

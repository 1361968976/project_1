<template>
  <div class="counter-container">
    <div class="less" @click="lessCount">-</div>
    <input type="text" v-model="goodsCount" />
    <div class="add" @click="addCount">+</div>
  </div>
</template>

<script>
import bus from "../eventBus.js";
export default {
  props: {
    goodsCount: {
      default: 0,
      type: Number,
    },
    goodsid: {
      default: 0,
      type: Number,
    },
  },
  data() {
    return {};
  },
  methods: {
    addCount() {
      const obj = { id: this.goodsid, value: this.goodsCount + 1 };
      bus.$emit("NewGoodsInfoAdd", obj);
    },
    lessCount() {
      const obj = { id: this.goodsid, value: this.goodsCount - 1 };
      bus.$emit("NewGoodsInfoLess", obj);
    },
  },
  watch: {
    productCount: {
      handler(newVal, oldVal) {
        this.$emit("newCount", newVal);
      },
      immediate: true,
    },
  },
};
</script>

<style lang="less" scope>
.counter-container {
  display: flex;
  margin-bottom: 10px;
  padding-right: 20px;
}
.counter-container input {
  width: 30px;
  height: 25px;
  outline: none;
  border: 1px solid #ccc;
  text-align: center;
  color: #ccc;
}
.less,
.add {
  width: 30px;
  text-align: center;
  height: 25px;
  line-height: 25px;
  color: #ccc;
  border: 1px solid #ccc;
  box-shadow: 0 0 3px 0 rgb(174 174 174);
}
</style>
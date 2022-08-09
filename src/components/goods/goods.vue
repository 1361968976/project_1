<template>
  <div class="goods-container">
    <input
      :checked="status"
      @change="stateChange"
      :id="'check' + id"
      type="checkbox"
      style="margin: 0 10px"
    />
    <label :for="'check' + id">
      <img id="logo" :src="img" />
    </label>
    <div class="text">
      <p>{{ title }}</p>
      <div class="price">
        <span>￥{{ singalPrice }}</span>
        <slot>abc</slot>
        <Counter :goodsid="id" :goodsCount="count"></Counter>
      </div>
    </div>
  </div>
</template>

<script>
import Counter from "../Counter/Counter";
export default {
  props: {
    id: {
      require: true,
      type: Number,
    },
    status: {
      default: "",
      type: Boolean,
    },
    title: {
      default: "",
      type: String,
    },
    img: {
      default: "",
      type: String,
    },
    singalPrice: {
      default: 0,
      type: Number,
    },
    count: {
      default: 0,
      type: Number,
    },
  },
  data() {
    return {};
  },
  methods: {
    stateChange(e) {
      const newState = e.target.checked;
      console.log(newState);
      this.$emit("stateChange", { id: this.id, value: newState });
    },
  },
  components: {
    Counter,
  },
};
</script>

<style lang="less" scope>
.goods-container {
  display: flex;
  width: 100%;
  height: 100px;
  flex-direction: row;
  justify-content: space-between;
  border-bottom: 1px solid #e0e0e0;
  margin: 10px 0;
}
#logo {
  margin: 0 10px;
  height: 90%;
}
.text {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  flex: 1;
  font-size: 13px;
}
.price {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
</style>
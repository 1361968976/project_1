<template>
  <div class="footer-container">
    <div class="left">
      <input :checked="allState" @change="noAllState" type="checkbox" />
      <span>全选</span>
    </div>
    <div class="mid">
      <span>合计:</span>
      <h4>￥{{ AllPrice }}</h4>
    </div>
    <div class="right">结算({{ totalCount }})</div>
  </div>
</template>

<script>
export default {
  props: {
    allState: {
      default: "",
      type: Boolean,
    },
    AllPrice: {
      default: 0,
      type: Number,
    },
    totalCount: {
      default: 0,
      type: Number,
    },
  },
  methods: {
    noAllState(e) {
      const allState = e.target.checked;
      console.log(e.target.checked);
      this.$emit("isAllState", allState);
    },
  },
};
</script>

<style lang="less" scope>
.footer-container {
  display: flex;
  width: 100%;
  height: 50px;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  background-color: white;
  color: #333;
}
.mid {
  flex: 1;
  display: flex;
  flex-direction: row;
  align-items: center;
}

.left {
  width: 30%;
  padding-left: 20px;
}
.left span {
  margin-left: 10px;
}
.right {
  width: 30%;
  height: 40px;
  text-align: center;
  line-height: 40px;
  background-color: rgb(109, 109, 255);
  border-radius: 20px;
  margin-right: 10px;
  color: white;
}
</style>
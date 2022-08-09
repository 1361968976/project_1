<template>
  <div class="header-container">{{ title }}</div>
</template>

<script>
export default {
  props: {
    title: {
      deafult: "",
      type: String,
    },
  },
};
</script>

<style lang="less" scope>
.header-container {
  font-size: 14px;
  height: 45px;
  width: 100%;
  color: white;
  line-height: 45px;
  text-align: center;
  background-color: rgb(109, 109, 255);
}
</style>
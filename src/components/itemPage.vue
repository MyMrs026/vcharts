<template>
  <div class="item">
    <!-- 设置插槽 -->
     <slot></slot>
  </div>
</template>

<script>

export default {
  name: "",
  data() {
    return {};
  },
};
</script>
<style lang="less" scoped>
.item{
  height:5.125rem;
  border: 1px solid blue;
  margin:.25rem;
  background-color: rgba(12,130,255,.85);
}
</style>

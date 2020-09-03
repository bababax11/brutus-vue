<template>
  <header>
    <div class="header-inner">
      <span>wasmオセロ</span>
      <!-- <img src="/icons/GitHub.png" width="24" height="24"/> -->
    </div>
  </header>
</template>
<script>
export default {}
</script>
<style lang="scss" scoped>
.header-inner {
  width: 576px;
  display: flex;
  align-items: baseline;
}
span {
  size: 36;
}
header {
  width: 100vw;
  height: 72;
  display: flex;
  padding: 0 0 calc((100vw - (100vw * 0.11 * 8)) / 2)
    calc((100vw - (100vw * 0.11 * 8)) / 2);
}
</style>

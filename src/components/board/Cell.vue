<template>
  <div
    :class="{ white: stone <= -1, black: stone >= 1 }"
    @click="$emit('click')"
  />
</template>
<script>
export default {
  props: {
    stone: {
      type: Number,
      required: true
    }
  }
}
</script>
<style lang="scss" scoped>
.white {
  border-radius: 35px;
  background-color: white;
}
.black {
  border-radius: 35px;
  background-color: black;
}
div {
  min-width: 35px;
  min-height: 35px;
}
</style>

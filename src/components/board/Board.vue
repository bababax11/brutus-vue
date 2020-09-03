<template>
  <div>
    <div v-for="(row, i) in game.board" :key="i" class="container">
      <div v-for="(s, j) in row" :key="j" class="frame">
        <Cell :stone="s" @click="_select(i, j)" />
      </div>
    </div>
  </div>
</template>
<script>
import { GameState } from "@/game_state"
export default {
  components: {
    Cell: () => import("./Cell")
  },
  props: {
    game: GameState
  },
  data: function() {
    return {
      X_SIZE: 7,
      Y_SIZE: 5
    }
  },
  methods: {
    _select(i, j) {
      this.$emit("select", i, j)
      this.$forceUpdate()
    }
  }
}
</script>
<style lang="scss" scoped>
.container {
  display: flex;
  justify-content: center;
}
.frame {
  border: 1px solid black;
  background-color: green;
}
</style>

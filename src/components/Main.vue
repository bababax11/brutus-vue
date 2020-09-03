<template>
  <main>
    <div class="center">
      <!-- <TopPanel /> -->
      <span>{{ message ? message : turn }}</span>
      <Board :game="game" @select="select" />
    </div>
  </main>
</template>
<script>
import { GameState } from "@/game_state"
export default {
  components: {
    // TopPanel: () => import("./board/TopPanel"),
    Board: () => import("./board/Board")
  },
  data() {
    return {
      game: new GameState(),
      selected: null,
      message: ""
    }
  },
  computed: {
    turn() {
      return this.game.turn === 1 ? "先手番です" : "後手番です"
    }
  },
  methods: {
    select(i, j) {
      console.log(101, i, j)
      if (!this.selected) {
        this.selected = [i, j]
        return
      }
      const [si, sj] = this.selected
      if (Math.abs(si - i) > 2 || Math.abs(sj - j) > 1) {
        this.selected = null
        return
      }
      const d = [i - si, j - sj]
      let state
      try {
        console.log(si, sj, d)
        state = this.game.moveDVec(si, sj, d)
        this.$forceUpdate()
        console.log(this.game.board)
      } catch (e) {
        console.log(this.game.board)
        console.log(e)
        this.selected = null
        return
      }
      this.selected = null
      if (state === 1) {
        this.message = "先手勝利です"
      } else if (state === -1) {
        this.message = "後手勝利です"
      }
    }
  }
}
</script>
<style lang="scss" scoped>
.center {
  text-align: center;
}
</style>

<template>
  <main>
    <div>
      <!-- <TopPanel /> -->
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
      selected: null
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
      // let state
      try {
        console.log(si, sj, d)
        this.game.moveDVec(si, sj, d)
        console.log(this.game.board)
        this.$forceUpdate()
        console.log(this.game.board)
      } catch (e) {
        console.log(this.game.board)
        console.log(e)
        this.selected = null
        return
      }
      this.selected = null
    }
  }
}
</script>
<style lang="scss" scoped>
// main {
//   display: flex;
//   padding: 40 10;
// }
</style>

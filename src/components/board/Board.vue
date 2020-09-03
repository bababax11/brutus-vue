<template>
  <div class="board">
    <div v-for="(row, i) in game.board" :key="i" class="container">
      <div v-for="(s, j) in row" :key="j" class="frame">
        <Cell
          :stone="s"
          :selected="selected && i === selected[0] && j === selected[1]"
          :legal="is_legal(i, j)"
          @click="_select(i, j)"
        />
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
    game: GameState,
    selected: {
      type: Array,
      default: null
    }
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
    },
    is_legal(i, j) {
      if(!this.selected)return false
      if(this.game.board[i][j] != 0)return false
      const di = i - this.selected[0], dj = j - this.selected[1]
      if(Math.abs(di) <= 1 && Math.abs(dj) <= 1)return true
      if(this.game.n_turns > 0 && di == this.game.turn * -2 && dj == 0)return true
      return false
    }
  }
}
</script>
<style lang="scss" scoped>
.board {
  margin: 10px;
}
.container {
  display: flex;
  justify-content: center;
}
.frame {
  border: 1px solid black;
  background-color: rgb(180, 151, 21);
}
</style>

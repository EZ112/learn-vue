

<script>
import Board from "./components/Board.vue";
import Scoreboard from "./components/Scoreboard.vue";
export default {
  data() {
    return {
      xScore: 0,
      oScore: 0,
    };
  },
  methods: {
    addScore(winner) {
      winner === "x-sign" ? this.xScore++ : this.oScore++;
    },
  },
  components: { Board, Scoreboard },
};
</script>

<template>
  <Scoreboard :xScore="xScore" :oScore="oScore" />
  <Board @score="addScore" />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: grid;
  align-items: center;
  justify-content: center;
}
</style>

<script>
import BoardBox from "./BoardBox.vue";

const INIT_BOXES = [
  { sign: null },
  { sign: null },
  { sign: null },
  { sign: null },
  { sign: null },
  { sign: null },
  { sign: null },
  { sign: null },
  { sign: null },
];

export default {
  data() {
    return {
      turn: Math.floor(Math.random() * 2),
      filledBox: 0,
      winner: null,
      boxes: [...INIT_BOXES],
    };
  },
  components: {
    BoardBox,
  },
  methods: {
    changeTurn(index) {
      let box = this.boxes[index];
      if (box.sign === null) this.turn = !this.turn;
      this.filledBox++;
    },
    selectBox(index) {
      this.boxes[index] = {
        ...this.boxes[index],
        sign: this.turn ? "x-sign" : "o-sign",
      };
    },
    checkBoard() {
      const winnerComb = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];
      const comb = winnerComb.filter((comb) => {
        const [sign1, sign2, sign3] = [
          this.boxes[comb[0]].sign,
          this.boxes[comb[1]].sign,
          this.boxes[comb[2]].sign,
        ];
        return sign1 && sign1 === sign2 && sign1 === sign3;
      });
      if (comb.length) {
        this.filledBox = 0;
        this.winner = this.boxes[comb[0][0]].sign;
        alert(this.winner[0] + " is the Winner");
        this.$emit("score", this.winner);
        this.boxes = [...INIT_BOXES];
      }
      if (this.filledBox === 9) {
        this.filledBox = 0;
        alert("Draw");
        this.boxes = [...INIT_BOXES];
      }
    },
  },
  emits: ["score"],
  updated() {
    this.checkBoard();
    console.log(this.filledBox);
  },
};
</script>

<template>
  <div class="turn">
    <div v-if="turn" class="sign o-sign" />
    <div v-else class="sign x-sign" />
    Turn
  </div>
  <div class="board">
    <BoardBox
      v-for="(box, index) in boxes"
      :key="index"
      :sign="box.sign"
      @click="
        changeTurn(index);
        selectBox(index);
      "
    />
  </div>
</template>



<style>
.board {
  display: grid;
  grid-template-columns: repeat(3, auto);
  gap: 5px;
  width: 500px;
  height: 500px;
  background: #333;
}
.turn {
  justify-self: center;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 20%;
  margin: 0 0 20px 0;
  padding: 10px 5px;
  border: 2px solid #333;
  border-radius: 5px;
}
.turn .sign {
  height: 25px;
  width: 25px;
  box-sizing: border-box;
  margin: 0 15px 0 0;
}
</style>
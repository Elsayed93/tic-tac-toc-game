<template>
  <h3 v-if="!endGame">
    <u class="player">{{ player }}</u> play ,,
  </h3>
  <h3 v-else>
    Game Ended, <u class="player">{{ lastValue }}</u> wins ,,
  </h3>
  <div class="game-container">
    <div class="box" @click.stop="fillBox" data-i="0" data-j="0">
      {{ container[0][0] }}
    </div>
    <div class="box" @click.stop="fillBox" data-i="0" data-j="1">
      {{ container[0][1] }}
    </div>
    <div class="box" @click.stop="fillBox" data-i="0" data-j="2">
      {{ container[0][2] }}
    </div>
    <div class="box" @click.stop="fillBox" data-i="1" data-j="0">
      {{ container[1][0] }}
    </div>
    <div class="box" @click.stop="fillBox" data-i="1" data-j="1">
      {{ container[1][1] }}
    </div>
    <div class="box" @click.stop="fillBox" data-i="1" data-j="2">
      {{ container[1][2] }}
    </div>
    <div class="box" @click.stop="fillBox" data-i="2" data-j="0">
      {{ container[2][0] }}
    </div>
    <div class="box" @click.stop="fillBox" data-i="2" data-j="1">
      {{ container[2][1] }}
    </div>
    <div class="box" @click.stop="fillBox" data-i="2" data-j="2">
      {{ container[2][2] }}
    </div>
  </div>

  <button v-if="endGame" @click="newGame">New Game</button>
</template>

<script>
export default {
  data() {
    return {
      lastValue: "",
      player: "O",
      endGame: false,
      container: [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""],
      ],
    };
  },
  methods: {
    fillBox(e) {
      if (!this.endGame) {
        let i = e.target.getAttribute("data-i");
        let j = e.target.getAttribute("data-j");
        this.container[i][j] = this.lastValue == "O" ? "X" : "O";
        this.player = this.player == "O" ? "X" : "O";
        this.lastValue = this.container[i][j];
      }
    },

    allEqual(arr) {
      return arr.every((v) => v === arr[0]);
    },

    resetGame() {
      this.container = [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""],
      ];
    },

    newGame() {
      this.endGame = false;
      this.lastValue = "";
      this.player = "O";
      this.resetGame();
    },

    // draw() {
    //   let fillAllBoxesWithoutWinner = this.container.every(checkAge);

    //   function checkAge(item) {
    //     return item !== "";
    //   }
    // },
  },

  updated() {
    if (this.allEqual(this.container[0]) && this.container[0][0] !== "") {
      this.endGame = true;
    }

    if (this.allEqual(this.container[1]) && this.container[1][0] !== "") {
      this.endGame = true;
    }

    if (this.allEqual(this.container[2]) && this.container[2][0] !== "") {
      this.endGame = true;
    }

    // first column
    if (
      this.allEqual([
        this.container[0][0],
        this.container[1][0],
        this.container[2][0],
      ]) &&
      this.container[0][0] !== ""
    ) {
      this.endGame = true;
    }

    // second column
    if (
      this.allEqual([
        this.container[0][1],
        this.container[1][1],
        this.container[2][1],
      ]) &&
      this.container[0][1] !== ""
    ) {
      this.endGame = true;
    }

    // third column
    if (
      this.allEqual([
        this.container[0][2],
        this.container[1][2],
        this.container[2][2],
      ]) &&
      this.container[0][2] !== ""
    ) {
      this.endGame = true;
    }

    // diameter1
    if (
      this.allEqual([
        this.container[0][0],
        this.container[1][1],
        this.container[2][2],
      ]) &&
      this.container[0][0] !== ""
    ) {
      this.endGame = true;
    }

    // diameter2
    if (
      this.allEqual([
        this.container[0][2],
        this.container[1][1],
        this.container[2][0],
      ]) &&
      this.container[0][2] !== ""
    ) {
      this.endGame = true;
    }

    // draw 1
    let draw1 = this.container[0].every((item) => {
      return item !== "";
    });

    // draw 1
    let draw2 = this.container[1].every((item) => {
      return item !== "";
    });

    // draw 1
    let draw3 = this.container[2].every((item) => {
      return item !== "";
    });

    // all boxes were filled and no winner
    if (draw1 && draw2 && draw3) {
      this.endGame = true;
      this.lastValue = "No one";
    }
    //
  },
};
</script>

<style>
.game-container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr;
  width: 300px;
  height: 300px;
}

.box {
  border: solid 1px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.8rem;
}

button {
  margin-top: 1rem;
}

.player {
  background-color: #b98bd1;
  padding: 0.25rem;
  border-radius: 0.25rem;
}
</style>
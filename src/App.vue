<template>
  <div id="app">
    <header>
      <h1>{{ message }}</h1>
    </header>
    <board v-bind:spaces="spaces" v-on:space-selected="spaceSelected" v-bind:disabled="isGameOver" />
    <button v-on:click="reset">Reset</button>
  </div>
</template>

<script>
import * as chunk from 'lodash.chunk';
import Board from "./components/Board.vue";

const players = ['X', 'O'];
const boardSize = 3;
const gameResultEnum = {
  X: Symbol('x-win'),
  O: Symbol('o-win'),
  draw: Symbol('draw')
};

export default {
  name: "app",
  components: {
    Board
  },
  data: function() {
    return {
      moveLog: []
    };
  },
  created: async function() {
    this.reset();
  },
  methods: {
    reset() {
      this.moveLog = [];
    },
    spaceSelected(spaceIndex) {
      if (!this.moveLog.some(i => i === spaceIndex)) {
        this.moveLog.push(spaceIndex);
      }
    },
    playerForLogIndex(index) {
      return players[index % 2];
    },
    hasRowWin(player) {
      const selectedSpaceRows = this.selectedSpaceRows(player);
      
      const rowScores = selectedSpaceRows.map(row => row.reduce((sum, v) => sum + v, 0));

      if (rowScores.some(score => score === boardSize)) {
        return true;
      }
    },
    hasColumnWin(player) {
      const selectedSpaceRows = this.selectedSpaceRows(player);

      const columnScores = Array(boardSize).fill(0);
      for (const row of selectedSpaceRows) {
        row.forEach((col, index) => {
          columnScores[index] += col;
        });
      }
      if (columnScores.some(score => score === boardSize)) {
        return true;
      }
    },
    hasDiagonalWin(player) {
      const selectedSpaceRows = this.selectedSpaceRows(player);
      
      const diagonalScores = Array(2).fill(0); // Squares have exactly 2 diagonals
      selectedSpaceRows.forEach((row, index) => {
        diagonalScores[0] += selectedSpaceRows[index][index];
        diagonalScores[1] += selectedSpaceRows[selectedSpaceRows.length - index - 1][index];
      });
      if (diagonalScores.some(score => score === boardSize)) {
        return true;
      }
    },
    selectedSpaceRows(player) {
      const selectedSpaces = this.spaces.map(s => s === player ? 1 : 0);
      return chunk(selectedSpaces, boardSize);
    }
  },
  computed: {
    currentPlayer() {
      return this.playerForLogIndex(this.moveLog.length);
    },
    isGameOver() {
      return !!this.gameResult;
    },
    gameResult() {
      for (const player of players) {
        if (
          this.hasRowWin(player) ||
          this.hasColumnWin(player) ||
          this.hasDiagonalWin(player)
        ) {
          return gameResultEnum[player];
        } else if (this.allSpacesAreFilled) {
          return gameResultEnum.draw;
        }
      }
    },
    gameResultMessage() {
      switch(this.gameResult) {
        case gameResultEnum.X:
          return 'Player X wins!';
        case gameResultEnum.O:
          return 'Player O wins!';
        case gameResultEnum.draw:
          return 'It\'s a draw!';
      }
    },
    message() {
      if (!this.isGameOver) {
        return `Player ${this.currentPlayer}'s turn...`;
      } else {
        return this.gameResultMessage;
      }
    },
    moveLogByPlayer() {
      return this.moveLog.map((spaceIndex, index) => ({ player: this.playerForLogIndex(index), spaceIndex }));
    },
    spaces() {
      const spaces = Array(boardSize**2).fill('');
      
      for (const move of this.moveLogByPlayer) {
        spaces[move.spaceIndex] = move.player;
      }

      return spaces;
    },
    allSpacesAreFilled() {
      return this.spaces.every(s => s);
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

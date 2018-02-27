<template>
  <div class="board-container">
    <div class="board">
      <row
        v-for="(row, index) in board"
        :row="row"
        :rowIndex="index"
        :clickMethod="handleClick"
        :key="index"
      />
    </div>
  </div>
</template>

<script>
import Row from './Row';

export default {
  name: 'Board',
  components: {
    Row,
  },
  data() {
    return {
      // Have them build board with function
      board: [
        ['', '', ''],
        ['', '', ''],
        ['', '', ''],
      ],
      currentTurn: 'X',
    };
  },
  methods: {
    changeCell(rowIndex, cellIndex) {
      // Onclick, the cell is changed to either an X or O
      return this.board.map((row, mappedRowIndex) => {
        if (rowIndex === mappedRowIndex) {
          return row.map((cell, mappedCellIndex) => {
            if (mappedCellIndex === cellIndex && cell === '') {
              return this.currentTurn;
            }
            return cell;
          });
        }
        return row;
      });
    },
    changeTurn() {
      // Shows who's turn it currently is
      this.currentTurn = this.currentTurn === 'X' ? 'O' : 'X';
    },
    handleClick(rowIndex, cellIndex) {
      // Exits if board spot is already taken
      if (this.board[rowIndex][cellIndex] !== '') return 'Fuck off nerd';
      // Write new board
      this.board = this.changeCell(rowIndex, cellIndex);
      // Exit if win
      if (this.winCheck()) return alert('this dude won! ', this.currentTurn);

      this.changeTurn();

      return 'Success';
    },
    winCheck() {
      // All possible wins
      const wins = [
        [this.board[0][0], this.board[0][1], this.board[0][2]],
        [this.board[0][0], this.board[1][0], this.board[2][0]],
        [this.board[0][0], this.board[1][1], this.board[2][2]],
        [this.board[0][0], this.board[1][0], this.board[2][0]],
        [this.board[0][1], this.board[1][1], this.board[2][1]],
        [this.board[0][2], this.board[1][2], this.board[2][2]],
      ];
      // Checks to see if all items in win arr are the same
      return wins.reduce((curr, arr) => {
        if (curr) return true;
        return `${arr[0]}${arr[1]}${arr[2]}` === `${arr[0]}${arr[0]}${arr[0]}` && arr[0] !== '';
      }, false);
    },
  },
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.board-container {
  display: flex;
  align-content: center;
  justify-content: center;
  padding-bottom: 50px;
  cursor: pointer;
}
</style>

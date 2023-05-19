<script>
import SideBar from './SidebarView.vue'
import ChessBoard from './ChessBoardView.vue'

export default {
  name: 'ChessContainer',
  data() {
    return {
      moveList: !localStorage.getItem("moveList") ? [] : JSON.parse(localStorage.moveList),
      activeCell: !localStorage.getItem("activeCell") ? "" : localStorage.getItem("activeCell").replace(/['"]+/g, ''),
      hintCell: "",
      maps: {
        1: "h",
        2: "g",
        3: "f",
        4: "e",
        5: "d",
        6: "c",
        7: "b",
        8: "a"
      }
    }
  },
  methods: {
    setActive(column, row) {
      if (this.activeCell === this.combineString(column, row)) return this.activeCell = 0;
      this.addMove(this.combineString(column, row));
      this.activeCell = this.combineString(column, row);
      this.hintCell = "";
      localStorage.setItem("activeCell", JSON.stringify(this.activeCell));
    },
    addMove(move) {
      this.moveList.push(move);
      localStorage.setItem("moveList", JSON.stringify(this.moveList));
    },
    moveBack() {
      const current = this.moveList.indexOf(this.activeCell);
      if(current > 0) {
        this.activeCell = this.moveList[current - 1];
      }
    },
    moveForward() {
      let current = this.moveList.indexOf(this.activeCell);
      if(current < this.moveList.length - 1) {
        this.activeCell = this.moveList[current + 1];
      }
    },
    combineString(col, row) {
      return this.maps[row] + col.toString();
    },
    getHint() {
      let num1 = Math.floor(Math.random() * 8) + 1;
      let num2 = Math.floor(Math.random() * 8) + 1;
      this.hintCell = this.maps[num1] + num2.toString();
    },
    newGame() {
      this.hintCell = "";
      this.activeCell = "";
      this.moveList = [];
      localStorage.clear();
    }
  },
  components: {
    SideBar,
    ChessBoard 
  }
}
</script>

<template>
  <div class="board-container">
    <ChessBoard :maps="maps" :combineString="combineString" :addMove="addMove" :activeCell="activeCell" :hintCell="hintCell" :setActive="setActive"/>
    <SideBar :moveList=moveList :addMove="addMove" :moveBack="moveBack" :moveForward="moveForward" :getHint="getHint" :newGame="newGame"/>
  </div>
</template>

<style scoped>
  .board-container {
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: center;
  }
  @media screen and (max-width: 920px) {
    .board-container {
      flex-direction: column;
      align-items: center;
    }
  }
</style>

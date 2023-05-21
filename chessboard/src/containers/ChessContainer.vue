<script>
import SideBar from '../components/SidebarView.vue'
import ChessBoard from '../components/ChessBoardView.vue'

export default {
  name: 'ChessContainer',
  data() {
    return {
      moveList: !localStorage.getItem("moveList") ? [] : JSON.parse(localStorage.moveList),
      /* ActiveCell and ActiveIndex are a little redundant. If I continued building 
      *  this out, i'd eventually resort to just activeIndex and remove activeCell  
      *  but for now this works.
      */
      activeCell: !localStorage.getItem("activeCell") ? "" : localStorage.getItem("activeCell").replace(/['"]+/g, ''),
      activeIndex: !localStorage.getItem("activeIndex") ? 0 : JSON.parse(localStorage.getItem("activeIndex")),
      hintCell: "",
      /* 
      * Letter map to covert numbers to their corresponding letter. 
      * example:81 = A1 
      */
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
    /* 
    * Main Handler for boards click event. 
    * Sets active square and calls move logic
    */
    setActive(column, row) {
      // unselects active square and exits if same squre is picked twice in a row;
      if (this.activeCell === this.combineString(column, row)) return this.activeCell = 0;
      
      this.activeCell = this.combineString(column, row);
      localStorage.setItem("activeCell", JSON.stringify(this.activeCell));   
      
      this.addMove(this.combineString(column, row), null);
    },
    /* 
    * Main Handler for boards moves. 
    * I kind of think there's too much logic in here
    * if I were to continue to build this out, i'd 
    * definitely seperate the move and directon logic
    * but for now it works.
    */
    addMove(move, direction) {
      // Adds new move
      if(move) {
        this.moveList.push(move);
        this.activeIndex = this.moveList.length - 1;
        localStorage.setItem("activeIndex", this.activeIndex);

        this.checkScroll();
        localStorage.setItem("moveList", JSON.stringify(this.moveList));
      }

      // Moves backwards when the back arrow is clicked
      if(direction ==='back' && this.activeIndex > 0) {
        this.activeCell = this.moveList[this.activeIndex - 1];
        this.activeIndex = this.activeIndex - 1;
        localStorage.setItem("activeIndex", this.activeIndex);
      }

      // Moves forward
      if(direction ==='forward' && this.activeIndex < this.moveList.length - 1) {
        this.activeCell = this.moveList[this.activeIndex + 1];
        this.activeIndex = this.activeIndex + 1;
        localStorage.setItem("activeIndex", this.activeIndex);
      }

      this.hintCell = "";
      this.checkScroll();
    },
    combineString(col, row) {
      return `${this.maps[row]}${col.toString()}`;
    },
    /* This is a very dumb random move generator
    *  Fully aware it will eventually suggest an 
    *  active squre.
    */ 
    getHint() {
      const num1 = Math.floor(Math.random() * 8) + 1;
      const num2 = Math.floor(Math.random() * 8) + 1;
      this.hintCell = this.maps[num1] + num2.toString();
    }, 
    newGame() {
      this.hintCell = "";
      this.activeCell = "";
      this.activeIndex = 0;
      this.moveList = [];
      localStorage.clear();
    },
    /* 
    *  Auto Scroller is super annoying on non desktop views
    */
    checkScroll() {   
      const scrollDiv = document.getElementById("collapse");
      if (window.innerWidth > 920 && window.innerHeight > 920) {
        scrollDiv.scrollIntoView({ behavior: "smooth" });
      }
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
    <ChessBoard 
      :activeCell="activeCell" 
      :setActive="setActive"
      :hintCell="hintCell" 
      :combineString="combineString" 
      :maps="maps" 
    />
    <SideBar 
      :activeCell="activeCell" 
      :activeIndex="activeIndex" 
      :moveList="moveList" 
      :addMove="addMove" 
      :moveBack="moveBack" 
      :moveForward="moveForward" 
      :getHint="getHint" 
      :newGame="newGame"
    />
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

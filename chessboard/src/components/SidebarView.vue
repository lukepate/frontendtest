<script>
export default {
  name: 'SideBar',
  props: {
    moveList: Array,
    addMove: Function,
    moveBack: Function,
    moveForward: Function,
    getHint: Function,
    newGame: Function
  }
}
</script>

<template>
  <div class="container">
    <div  class="move-container">
      <div v-for="(move, index) in moveList" :key="index">
        {{ index + 1 }}: {{ move }}
      </div>
    </div>
    <div class="button-container">
      <button class="btn" @click="newGame()">
          <svg width="24" height="24" fill="none" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" clip-rule="evenodd" d="M12 5a1 1 0 0 1 1 1v12a1 1 0 1 1-2 0V6a1 1 0 0 1 1-1z" fill="#d0cfcf"/><path fill-rule="evenodd" clip-rule="evenodd" d="M5 12a1 1 0 0 1 1-1h12a1 1 0 1 1 0 2H6a1 1 0 0 1-1-1z" fill="#d0cfcf"/></svg>
      </button>
      <button class="btn" @click="moveBack()">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24"><path d="M15.293 3.293 6.586 12l8.707 8.707 1.414-1.414L9.414 12l7.293-7.293-1.414-1.414z"/></svg>
      </button>
      <button class="btn" @click="moveForward()">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24"><path d="M7.293 4.707 14.586 12l-7.293 7.293 1.414 1.414L17.414 12 8.707 3.293 7.293 4.707z"/></svg>
      </button>
      <button class="btn" @click="getHint()"> 
        <svg data-name="Layer 1" width="24" height="24" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 128 128"><path d="M36.293 53.875a27.936 27.936 0 0 1 26.85-25.961c.289-.009.576-.013.864-.013a27.761 27.761 0 0 1 27.756 27.763 27.909 27.909 0 0 1-13.576 23.859 7.833 7.833 0 0 0-3.825 6.683v3.032a.086.086 0 0 1-.085.086h-2.99l4.2-23.706v-.005l1.364-7.7a2 2 0 1 0-3.938-.7L71.677 64.2c-1.616 1.256-3.29.536-6.637-1.38-2.612-1.5-5.976-3.408-9.346-2.179l-.607-3.422a2 2 0 1 0-3.938.7l1.135 6.4 4.432 25h-2.99a.086.086 0 0 1-.085-.086v-3.028a7.764 7.764 0 0 0-3.778-6.653 27.71 27.71 0 0 1-13.57-25.677zm38.842 39.449a2.021 2.021 0 0 1 0 4.041h-22.27a2.021 2.021 0 0 1 0-4.041h22.27zm2.021 10.062a2.023 2.023 0 0 1-2.021 2.021h-22.27a2.021 2.021 0 0 1 0-4.042h22.27a2.023 2.023 0 0 1 2.021 2.021zM60.777 89.324l-4.36-24.6c1.644-1.07 3.372-.306 6.635 1.563 2 1.145 4.447 2.547 6.981 2.546a6.581 6.581 0 0 0 .833-.059l-3.643 20.55zm4.058 30.106h-1.669a3.984 3.984 0 0 1-3.442-1.982h8.554a3.984 3.984 0 0 1-3.444 1.983zm10.3-5.982h-22.27a2.021 2.021 0 1 1 0-4.041h22.27a2.021 2.021 0 1 1 0 4.041zM66 16.858V6.569a2 2 0 1 0-4 0v10.289a2 2 0 1 0 4 0zm-38.758 46.58a2 2 0 0 0-2-2H14.953a2 2 0 0 0 0 4h10.289a2 2 0 0 0 2-2zM32.291 33.5a2 2 0 0 0 0-2.828L25.016 23.4a2 2 0 0 0-2.828 2.828l7.275 7.272a2 2 0 0 0 2.828 0zm82.756 29.937a2 2 0 0 0-2-2h-10.289a2 2 0 0 0 0 4h10.289a2 2 0 0 0 2-1.999zM98.537 33.5l7.275-7.275a2 2 0 0 0-2.828-2.828l-7.275 7.275a2 2 0 1 0 2.828 2.828z"/></svg>      </button>
    </div>
  </div>
</template>

<style scoped>
  .container {
    display: flex;
    flex-direction: column;
    background-color: #41403e;
    max-width: 300px;
    width: 400px;
    min-height: 842px;
    height: 800px;
    overflow: auto;
    color: white;    
    margin: 0 30px;
  }
  .move-container {
    height: 100%;
  }
  .button-container {
    background-color: #383734;
    min-height: 100px;
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 4px;
  }
  .btn {
    aspect-ratio: 1/1;
    width: 50px;
    border: none;
    color: white;
    fill: #d0cfcf;
    background-color: #51504c;
    border-radius: 10%;
    cursor: pointer;
  }
  .new:before {
  }
  .chevron-left:before {
  }

  .chevron-right:before {
  }
  @media screen and (max-width: 1080px) {
    .container {
      margin: 0 0;
      flex-direction: row;
      margin-top: 50px;
      /* width: 100%;
      max-width: 100%;
      height: 100%;
      min-height: 300px; */
    }
  }
</style>

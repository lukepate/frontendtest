<script>
import SideBarButtons from './SideBarButtonView.vue'

export default {
  name: 'SideBar',
  props: {
    activeCell: String,
    activeIndex: Number,
    moveList: Array,
    addMove: Function,
    moveBack: Function,
    moveForward: Function,
    getHint: Function,
    newGame: Function
  },
  components: {
    SideBarButtons
  }
}
</script>

<template>
  <div class="container">
    <div class="user-container">
      <img alt="User Avatar" src="https://images.chesscomfiles.com/uploads/v1/user/66746068.6b0443e7.200x200o.431299f833ac.png" data-cy="chat-message-avatar" width="75" height="75" class="user-image" />
      <div class="chat-bubble-container">
        <div class="down-arrow"></div>
        <div class="chat-bubble">Hello, Pls hire me!</div>
      </div>
    </div>
      <div class="opening">
        Starting Position
    </div>
    <div  class="move-container">
      <ul class="move-list">
        <li class="move" v-for="(move, index) in moveList" :key="index">
          {{ index + 1 }}: 
          <span :class="this.activeCell === move && this.activeIndex === index? 'move-text move-active' : 'move-text'">{{ move }}</span>
        </li>
        <div :id="`collapse`"></div>
      </ul>

    </div>
    <SideBarButtons 
      :addMove="addMove" 
      :moveBack="moveBack" 
      :moveForward="moveForward" 
      :getHint="getHint" 
      :newGame="newGame" 
    />
  </div>
</template>

<style scoped>
  .container {
    display: flex;
    flex-direction: column;
    background-color: var(--main-dark-5);
    max-width: 300px;
    width: 400px;
    min-height: 865px;
    height: 800px;
    color: var(--main-light-1);    
    margin: 0 var(--space-xl);
  }
  .move-container {
    height: 100%;
  }
  .move-list {
    text-align: left;
    padding: 0;
    max-height: 530px;
    overflow-x: hidden;
    padding-bottom: var(--space-xl);
  }
  .move {
    list-style: none;
    background-color: var(--main-dark-5);
    padding: var(--space-sm) var(--space-lg);
    font-weight: var(--font-weight-md);
    color: var(--main-light-3, white);
  }
  .move:nth-child(even)  {
    background-color: var(--main-dark-3);
  }
  .move-text {
    padding: 0 var(--space-lg);
  }
  .move-active {
    background-color: var(--main-dark-6);
  }
  .opening {
    text-align: left;
    padding: 0 var(--space-lg);
    color: var(--main-light-3);
    font-weight: var(--font-bold);
    margin-top: 60px;
  }
  .user-image {
    border-radius: 10%;
    margin: var(--space-md);
  } 
  .chat-bubble{
    background-color: var(--main-dark-3);
    padding: var(--space-lg);
    border-radius: var(--space-md);
    margin-left: -6px;
  }

  .user-container {
    display: flex;
    margin-bottom: var(--space-xl);
  }
  .chat-bubble-container {
    display: flex;
    align-items: center;
  }
  .down-arrow {
    width: 0; 
    height: 0; 
    border-left: var(--space-md) solid transparent;
    border-right: var(--space-md) solid transparent;
    border-top: var(--space-md) solid  var(--main-dark-3);
    transform: rotate(.25turn);
    margin-top: -16px;
  }

  @media screen and (max-width: 920px) {
      .container {
        width: 84vw;
        height: 84vw;
        max-width: 100%;
        margin: 168px var(--space-xl);
      }
      .move-list {
        padding-bottom: 0;
      }
  }
</style>

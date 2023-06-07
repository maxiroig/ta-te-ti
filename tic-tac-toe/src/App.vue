<script setup>
import { ref } from 'vue';
import Game from './components/Game.vue';

let playerActive = null
let gameStarted = ref(false);

let playerShuffle = () => {
  return Math.random() < 0.5;
}
const startGame = () => {
    gameStarted.value = !gameStarted.value;
    let number = playerShuffle();
    if (number < 0.5){
      playerActive = "Player 1"
    }else{
      playerActive = "Player 2"
    }
};
</script>

<template>
  <header class="">
    <div class="text-center mb-8">
      <h1 class="text-5xl font-bold underline text-white">
        Welcome to the game
      </h1>
      <div>
        <button
        v-if="!gameStarted" 
        @click="startGame"
        class="mt-3 rounded-sm p-2 bg-emerald-600 text-black hover:bg-emerald-400">
          Start Game
        </button> 
        <button
        v-else
        @click="startGame"
        class="mt-3 rounded-sm p-2 bg-emerald-600 text-black hover:bg-emerald-400">
          Restart Game
        </button> 
      </div>
    </div>
  </header>
  <main 
  v-if="gameStarted"
  class="w-[800px] h-[800px] mx-auto">
    <Game :playerTurn="playerActive"/>
  </main>
</template>



<script setup>
  import { defineProps } from 'vue';

  defineProps({ yourScore: Number, playerName: String})

</script>

<template>
  <div id="#game-over-container">
    <h3>Game Over</h3>
    <h4>Good job {{ playerName }}! You got {{ yourScore }} points</h4>
    <button @click="$router.push('/')" id="try-again">Try Again</button>
  </div>
</template>

<style>
  #try-again {
  font-size: 2rem;
  font-family: digital;
  width: 15vw;
  border-radius: 0.5rem;
  padding: 0.5rem;
  color: white;
  background-image: linear-gradient(#060561, #383783);
  margin-top: 9rem;
  border-style: none;
  }

  #try-again:hover {
    background-image: linear-gradient(#282685, #444399);
    cursor: pointer;
  }

  #try-again:active {
    box-shadow: inset 0px 0px 10px rgba(0, 0, 0, 0.566);
  }

  @media (max-width: 1200px) {
    #try-again {
      width: 50vw;
    }
  }
</style>
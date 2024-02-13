<script setup>
import { ref } from 'vue';

let name = ref('')


function saveName() {
  localStorage.setItem('name', name.value)
}

function deleteName() {
  localStorage.clear('name')
  location.reload()
}

let savedName = localStorage.getItem('name')

</script>

<template>
  <div>
    <div v-if="savedName">
      <h3>Hello</h3>
      <h4>{{ savedName }}</h4>
      <button id="new-player" @click="deleteName">New player?</button>
    </div>
    <div v-else>
      <h3>What's your name?</h3>
      <form @submit="saveName">
      <input type="text" v-model="name">
      <button type="submit" id="save">save</button>
      </form>
    </div>
  </div>
</template>

<style>

  input {
    font-size: 1.5rem;
    font-family: digital;
    margin-top: 3rem;
    border-radius: 1rem;
    padding: 0.5rem;
    border-style: none;
 }

  #save {
    font-size: 1.5rem;
    font-family: digital;
    margin-left: 1rem;
    border-radius: 1rem;
    padding: 0.5rem;
    color: white;
    background-image: linear-gradient(#060561, #383783);
    border-style: none;
 }

  #save:hover {
    background-image: linear-gradient(#282685, #444399);
    cursor: pointer;
  }

  h3 {
    font-family: digital;
    font-size: 3rem;
    color: #060561;
  }

  h4 {
    font-family: digital;
    letter-spacing: 0.5rem;
    font-size: 3rem;
    margin-top: 2rem;
    color: white;
    text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.722);
  }

  #new-player {
    text-decoration: underline;
    font-size: 1rem;
    margin-top: 1rem;
    font-family: digital;
    border-style: none;
    background: none;
    color: #060561;
  }

  #new-player:hover {
    cursor: pointer;
    color: #282685;
  }

  @media (max-width: 800px) {
    h3 {
      font-size: 4rem;
    }

    h4 {
      font-size: 4rem;
    }

    #new-player {
      font-size: 1.5rem;
    }

    input {
      font-size: 1.8rem;
   }
  
    #save {
      font-size: 1.5rem;
      margin-top: 1rem;
   }
  
  }

  @media (min-width: 800px) and (max-width: 1200px) {
    h3 {
      font-size: 5rem;
    }

    h4 {
      font-size: 5rem;
    }

    #new-player {
      font-size: 2rem;
    }

    input {
      font-size: 3rem;
   }
  
    #save {
      font-size: 3rem;
   }
  
  }
</style>

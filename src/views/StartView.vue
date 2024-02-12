<script setup>
  import { RouterLink } from 'vue-router'
  import NameComponent from '../components/NameComponent.vue'
  
</script>

<template>
  <div id="name-container">
    <NameComponent></NameComponent>
  </div>
  <div id="link-container">
    <RouterLink to="/game" id="router-link">START</RouterLink>
  </div>
  
</template>

<style>

  #name-container {
    margin-top: 4rem;
    text-align: center;
  }


  #link-container {
    text-align: center;
    margin-top: 10rem;
    display: flex;
    justify-content: center;
  }

  #router-link {
    font-size: 5rem;
    background-image: linear-gradient(#060561, #383783);
    color: white;
    text-decoration: none;
    border-radius: 1rem;
    padding: 2rem;
    font-family: digital2;
    letter-spacing: 0.5rem;
    font-weight: 600;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.566);
    margin: 1rem;
  }

  #router-link:hover {
    background-image: linear-gradient(#282685, #444399);
  }

  #router-link:active {
    box-shadow: inset 0px 0px 10px rgba(0, 0, 0, 0.566);
  }

  @media (min-width: 800px) and (max-width: 1200px) {
    #link-container {
      margin-top: 20rem;
    }
  }

</style>
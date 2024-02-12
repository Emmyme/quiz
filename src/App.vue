<script setup>
import { RouterView } from 'vue-router'
import FooterComponent from '../src/components/FooterComponent.vue'
</script>

<template>
  <main>
    <RouterView/>
    <FooterComponent></FooterComponent>
  </main>
</template>

<style scoped>
@font-face {
  font-family: digital;
  src: url(./assets/Chakra_Petch/ChakraPetch-Regular.ttf);
}
@font-face {
  font-family: digital2;
  src: url(./assets/VT323/VT323-Regular.ttf);
}

main {
  display: flex;
  flex-direction: column;
  
}

</style>

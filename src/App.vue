<script setup>
import Grid from './components/Grid.vue';


</script>

<template>
  <main>
    <Grid />
  </main>
</template>

<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: row;
  height: 100vh;
  background-color: var(--background-color);
}
</style>

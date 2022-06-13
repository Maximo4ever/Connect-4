<script setup>
  import { provide, ref } from 'vue';
  import Table from './components/Table.vue';

  const totalWins = ref({
    red: 0,
    yellow: 0
  });
  provide("totalWins", totalWins)
</script>

<template>
  <div class="winsContainer">
    <div>
      <h3 class="player redPlayer">Red Player</h3>
      <span>{{totalWins.red}}</span>
    </div>
    <div>
      <h3 class="player yellowPlayer">Yellow Player</h3>
      <span>{{totalWins.yellow}}</span>
    </div>
  </div>
  <Table />
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-family: 'Poppins', sans-serif;
}
.winsContainer {
  width: 508px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-inline: 20px;
  margin-bottom: 20px;
}
.winsContainer div {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  font-size: 24px;
}
.player {
  text-shadow: 2px 2px 3px #000;
}
.redPlayer {
  color: red;
}
.yellowPlayer {
  color: rgb(255, 255, 0);
}
</style>

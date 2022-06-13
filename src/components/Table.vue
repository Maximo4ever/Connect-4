<script setup>
  import { inject, ref } from 'vue';
  import Column from './Column.vue';
  import { winner } from './IsWinner';

  const nameColumns = ["a","b","c","d","e","f","g"];
  const redPlayer = ref(true);
  const wins = inject("totalWins")
  
  const playToken = async (nameCol) => {
    const color = redPlayer.value ? "red" : "yellow";
    const column = [...document.querySelectorAll(`.col-${nameCol} [status=empty]`)];
    const lastSlot = column.length-1;
    column[lastSlot].setAttribute("status", color);
      
    // Ejecuta la animacion de la ficha cayendo
    await ballAnimation(column, color);
    // Pinta la ultima ficha
    column[lastSlot].style.background = color;
    // Cambia el turno
    redPlayer.value = !redPlayer.value;

    winner((winner) => {  
      if (winner !== null) wins.value[winner] += 1;
      console.log(winner);
    });
  }
  
  const ballAnimation = async (column, color) => {
    for (let i = 0; i < column.length; i++) {
      let element = column[i];
      // Crea efecto de animacion 
      await timer(i*10, element, color); 
      setTimeout(async() => {
        await timer(i*10, element, "#FFFFFF");
      }, 30);
    };
  }
  const timer = (ms, element, color) => {
    return new Promise((res) => {
      setTimeout(() => {
        if (element.getAttribute("status") == "red" || element.getAttribute("status") == "yellow") {
          return res() 
        }
        element.style.background = color;
        return res()
      }, ms)
    });
  }
</script>
<template>
  <div class="table">
    <Column v-for="(nameCol) in nameColumns" :nameCol="nameCol" @click="playToken(nameCol)" />
  </div>
</template>
<style>
.table {
  display: flex;
  column-gap: 10px;
  background-color: #4B7DBA;
  border: 2px solid #073976;
  padding: 30px;
}
</style>
<script setup>
  import { inject, ref } from 'vue';
  import Column from './Column.vue';
  import { winner } from './IsWinner';

  const nameColumns = ["a","b","c","d","e","f","g"];
  const redPlayer = ref(true);
  const totalWins = inject("totalWins")
  
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

    winner((winner, winSlots) => {  
      if (winner === null) return
      totalWins.value[color] += 1;
      winSlots.forEach((winSlot) => winSlot.style.borderColor = "#FFFFFF");
      setTimeout(() => {
        restartGame()
      }, 1500);

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
  const restartGame = () => {
    const column = [...document.querySelectorAll(".slot")];
    column.forEach((elementSlot) => {
      elementSlot.setAttribute("status", "empty");
      elementSlot.style.background = "#FFFFFF";
    });
  }
  const resetCounter = () => {
    totalWins.value = {
      red: 0,
      yellow: 0
    }
  }
</script>
<template>
  <div class="table">
    <Column v-for="(nameCol) in nameColumns" :nameCol="nameCol" @click="playToken(nameCol)" />
  </div>
  <div class="resetsContainer">
    <button @click="restartGame">Restart Game</button>
    <button @click="resetCounter">Reset Counter</button>
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
.resetsContainer {
  width: 508px;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  margin-top: 20px;
}
.resetsContainer button {
  cursor: pointer;
  font-size: 20px;
  padding: 12px 20px;
  background-color: #4f555f;
  color: #fff;
  border: none;
  box-shadow: 0.8px 3.8px 5.3px -21px rgb(0 0 0 / 10%), 6px 30px 42px -21px rgb(0 0 0 / 20%)
}
</style>
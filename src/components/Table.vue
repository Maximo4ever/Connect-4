<script setup>
  import { ref } from 'vue';
  import Column from './Column.vue';

  const nameColumns = ["a","b","c","d","e","f","g"];
  const table = ref([])
  const redPlayer = ref(true)
  
  const playToken = ({target}, nameCol, index) => {
    const color = redPlayer.value ? "red" : "yellow";
    const column = [...document.querySelectorAll(`.col-${nameCol} [status=empty]`)];
    const lastSlot = column.length-1;
    column[lastSlot].setAttribute("status", color);
    column[lastSlot].style.background = color;
    redPlayer.value = !redPlayer.value;

    table.value.push(column[lastSlot]);
    console.log(table.value);
  }
</script>
<template>
  <div class="table">
    <Column v-for="(nameCol,index) in nameColumns" :nameCol="nameCol" @click="playToken($event, nameCol)" />
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
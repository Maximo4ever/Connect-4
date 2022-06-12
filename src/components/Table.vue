<script setup>
  import Column from './Column.vue';
  const nameColumns = ["a","b","c","d","e","f","g"]
</script>
<template>
  <div class="table">
    <Column v-for="nameCol in nameColumns" :nameCol="nameCol" />
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
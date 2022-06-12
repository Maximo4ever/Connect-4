<script setup>
  defineProps({
    slot: Object
  });
</script>
<template>
  <div 
    class="slot" 
    :class="slot.name+slot.index" 
    status="empty"
  >
  </div>
</template>
<style>
  .slot {
    width: 55px;
    height: 55px;
    background: #fff;
    border: 2px solid #073976;
    border-radius: 50%;
    cursor: pointer;
  }
</style>
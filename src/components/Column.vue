<script setup>
  import Slot from './Slot.vue'
  defineProps({
    nameCol: String
  })
  const indexSlots = [1,2,3,4,5,6,7]
</script>
<template>
    <div class="col" :class="'col-'+nameCol">
      <Slot v-for="(n,index) in indexSlots" :slot="{name:nameCol,index: index+1}" />
    </div>
</template>
<style>
.col {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  row-gap: 10px;
}
.ballAnimationRed {
  background-color: #ff0000;
}
.ballAnimationYellow {
  background-color: #ffff00;
}
</style>
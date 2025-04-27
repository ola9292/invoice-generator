<script setup>
  import Invoice from './components/Invoice.vue';
  import { ref } from 'vue';
  import Landing from './components/Landing.vue';

  const start = ref(false)
  const toggleStart = () => {
    start.value = !start.value
  }

</script>

<template class="">
  <div class="main-container">
    <!-- <h1 style="text-align: center;">Invoice Maker</h1> -->
      <Landing v-if="!start" @toggle-start="toggleStart"/>
     <Invoice v-if="start"/>
  </div>
  
</template>

<style>
 
</style>

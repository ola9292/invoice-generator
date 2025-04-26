<script setup>
  import Invoice from './components/Invoice.vue';
  import { ref } from 'vue';

  // const darkTheme = ref(false)
  // const theme = ref("dark")

  // const changeTheme = () => {
  //   darkTheme.value = !darkTheme.value
  // }
</script>

<template class="">
  <div class="main-container">
    <h1 style="text-align: center;">Invoice Generator</h1>
    <Invoice />
  </div>
  
</template>

<style>
 
</style>

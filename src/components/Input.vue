<template>
    <div class="blockInp">
      <input min="0" type="number" @input="changeAmount($event.target.value)" />
      <button @click="convert()">convert</button>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      changeAmount: {
        type: Function,
        required: true
      },
      convert: {
        type: Function,
        required: true
      }
    }
  }
  </script>
  
  <style scoped>
  
  
  
  </style>
  
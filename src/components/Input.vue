<template>
    <div className="blockInp">
    <input min="0" type="number" @input="changeAmount($event.target.value)">
    <button @click="convert()">convert</button>
</div>
  </template>
  
  <script>
  
  
  export default{
   props:{
    changeAmount:{   
        type: Function,
        required: true
    },
    convert:{   
        type: Function,
        required: true
    }
   }
  }
  </script>
  
  <style scoped>
.blockInp{
    display: flex;
    flex-direction: column;
    align-items: center;
}

button{
    position: relative;
    top: -20px;
    padding: 15px 20px;
    color: #fff;
    text-transform: uppercase;
    cursor: pointer;
    background: #1a032d;
    border: 0;
    border-radius: 3px;
    text-align: center;
}

   input {
    outline: none;
    width: 500px;
    position: relative;
    top: -50px;
    font-size: 1.2em;
    border-radius: 3px;
    border: 0;
    padding: 10px 15px;
    background: #fafafa;
    color: #333;
   }
  </style>
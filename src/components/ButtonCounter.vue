<template>
    <button @click="count++">
      You clicked me {{ count }} times.
    </button>
  </template>
  
  <script>
  export default {
    data() {
      return {
        count: 0,
      };
    },
  };
  </script>
  
  <style scoped>
  button {
    padding: 10px 20px;
    background-color: lightblue;
    border: none;
    cursor: pointer;
  }
  </style>
  
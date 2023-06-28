<template>
    <div class="calculator">
      <input type="text" v-model="display" disabled />
      <div class="buttons">
        <button v-for="button in buttons" :key="button" @click="handleButton(button)">{{ button }}</button>
        <button @click="calculateResult()">=</button>
        <button @click="setB">Reset</button>
      </div>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    name: 'App',
    setup() {
      const display = ref(''); // Store the display value
  
      const buttons = [
        '1', '2', '3', '+',
        '4', '5', '6', '-',
        '7', '8', '9', '*',
        '0', '.', '/',
      ];
  
      // Method to handle button clicks
      const handleButton = (button) => {
        display.value += button;
      };    
      const setB=()=>{
        display.value=''
      }
  
      // Method to calculate the result
      const calculateResult = () => {
        try {
          const result = eval(display.value); // Use eval() to evaluate the expression
          display.value = result;
        //   display.value=''
        } catch (error) {
          display.value = 'Error';
        }
      };
  
      return {
        display,
        buttons,
        handleButton,
        calculateResult,
        setB
      };
    },
  };
  </script>
  
  <style scoped>
  .calculator {
    max-width: 200px;
    margin: 0 auto;
  }
  
  .buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 10px;
    margin-top: 10px;
  }
  
  button {
    padding: 10px;
    font-size: 16px;
  }
  </style>
  
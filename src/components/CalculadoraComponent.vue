<template>
    <div>
    <div id="app">
        <h1>Calculadora Vue.js 3.0</h1>
        
        <div class="calculator">
        <div class="display" id="display">
            {{ calculate }}
        </div>
        <div class="input">
            <input type="text" v-model="firstNumber" placeholder="Primeiro">
            <select v-model="operation">
            <option value="+" selected>+</option>
            <option value="-">-</option>
            <option value="*">*</option>
            <option value="/">/</option>
            </select>
            <input type="text" v-model="secondNumber" placeholder="Segundo">
        </div>
        </div>
    </div>
    </div>
</template>

<script>
import { ref, computed } from 'vue';

export default {
    setup() {
        const firstNumber = ref('');
        const secondNumber = ref('');
        const operation = ref('+');

        const calculate = computed(() => {
        const num1 = parseFloat(firstNumber.value);
        const num2 = parseFloat(secondNumber.value);
        let result = 0;
        switch (operation.value) {
            case '+':
            result = num1 + num2;
            break;
            case '-':
            result = num1 - num2;
            break;
            case '*':
            result = num1 * num2;
            break;
            case '/':
            result = num1 / num2;
            break;
        }
        return isNaN(result) ? 0 : result;
        });

        const displayResult = computed(() => calculate.value === 0 ? '0' : calculate.value);

        return { firstNumber, secondNumber, operation, calculate, displayResult };
    }
};
</script>

<style>
#app {
    text-align: center;
}

h1 {
    margin-top: 0;
}

.display {
    height: 50px;
    background-color: #f2f2f2;
    margin-bottom: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 24px;
    border: 2px solid black;
    background-color: aqua;
}

.calculator {
    width: 300px;
    margin: 0 auto;
    text-align: center;
}

.input {
    display: flex;
    justify-content: center;
    align-items: center;
}

.input input, .input select {
    width: 100px;
    height: 30px;
    margin: 5px;
    font-size: 16px;
    border: 2px solid black;
}
</style>

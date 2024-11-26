
<script lang="ts">
import {defineComponent, ref} from 'vue';

export default defineComponent({
    name: 'Calculator',
    setup(){
        const display = ref<string>(''); //Show the actual value
        const firstNumber = ref<number | null>(null); //First numer
        const operation = ref<string | null>(null); //Operation (examples +,-,*,/)
        const secondNumber = ref<number | null>(null);

        const appendNumber = (num: number) => {
            display.value += num.toString();
        };

        const setOperation = (op:string ) => {
            if(display.value){
                firstNumber.value = parseFloat(display.value);
                display.value = ''
                operation.value = op;
                console.log(firstNumber.value)
            }
        }

        const calculate = () => {
            if (firstNumber.value !== null && operation.value && display.value){
                secondNumber.value = parseFloat(display.value);
                console.log(secondNumber.value)
                
                switch(operation.value){
                    case '+':
                        display.value = (firstNumber.value + secondNumber.value).toString();
                        console.log(display.value)
                        break;
                    
                    case '-':
                        display.value = (firstNumber.value - secondNumber.value).toString();
                        console.log(display.value)
                        break;
                    
                    case 'x':
                        display.value = (firstNumber.value * secondNumber.value).toString();
                        console.log(display.value)
                        break;

                    case '/':
                        if (secondNumber.value === 0) {
                        display.value = 'Error'; // Undvik division med 0
                        } else {
                        display.value = (firstNumber.value / secondNumber.value).toString();
                        }
                        break;
                }   

                firstNumber.value = null;
                operation.value = null;
                secondNumber.value = null;
            }
        }

        const clear = () => {
            display.value = '';
            firstNumber.value = null;
            operation.value = null;
            secondNumber.value = null;
        }

        return {
            display,
            firstNumber,
            operation,
            secondNumber,
            appendNumber,
            setOperation,
            calculate,
            clear
        };
    }

})
</script>

<template>
    <div class="calculator card container mt-4 bg-dark" style="width: 25rem;">
        <h2 style="text-align: center; color: white;">Miniräknare</h2>
        <div class="display bg-dark text-end p-3 mb-3" style="color: white">
            {{ display || '0' }}
        </div>
        <div class="buttons">
            <div class="row mb-2">
                <button class="btn btn-warning col-9" @click="clear">C</button>
                <button class="btn btn-secondary col-3" @click="setOperation('*')">/</button>
            </div>
            <div class="row mb-2">
                <button class="btn btn-primary col-3" @click="appendNumber(7)">7</button>
                <button class="btn btn-primary col-3" @click="appendNumber(8)">8</button>
                <button class="btn btn-primary col-3" @click="appendNumber(9)">9</button>
                <button class="btn btn-secondary col-3" @click="setOperation('x')">x</button>
            </div>
            <div class="row mb-2">
                <button class="btn btn-primary col-3" @click="appendNumber(4)">4</button>
                <button class="btn btn-primary col-3" @click="appendNumber(5)">5</button>
                <button class="btn btn-primary col-3" @click="appendNumber(6)">6</button>
                <button class="btn btn-secondary col-3" @click="setOperation('-')">-</button>
            </div>
            <div class="row mb-2">
                <button class="btn btn-primary col-3" @click="appendNumber(1)">1</button>
                <button class="btn btn-primary col-3" @click="appendNumber(2)">2</button>
            <button class="btn btn-primary col-3" @click="appendNumber(3)">3</button>
            <button class="btn btn-secondary col-3" @click="setOperation('+')">+</button>
            </div>
        <div class="row mb-2">
            <button class="btn btn-primary col-6">0</button>
            <button class="btn btn-secondary col-6" @click="calculate">=</button>
        </div>
        </div>
    </div>
</template>
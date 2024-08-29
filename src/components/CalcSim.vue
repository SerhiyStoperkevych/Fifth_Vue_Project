<template>
    <div>
        <h1>Calculator:</h1>
        <h2>{{ currentNum }}</h2>
        <p>{{ prevNum }}</p>
        <div>
            <button @click="addNum('0')">0</button>
            <button @click="addNum('1')">1</button>
            <button @click="addNum('2')">2</button>
            <button @click="addNum('3')">3</button>
            <button @click="addNum('4')">4</button>
            <button @click="addNum('5')">5</button>
            <button @click="addNum('6')">6</button>
            <button @click="addNum('7')">7</button>
            <button @click="addNum('8')">8</button>
            <button @click="addNum('9')">9</button>
        </div>
        <hr>
        <div>
            <button @click="addInt('+')">+</button>
            <button @click="addInt('-')">-</button>
            <button @click="addInt('*')">*</button>
            <button @click="addInt('/')">/</button>
            <button @click="calc">=</button>
            <button @click="clear">C</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'CalcSim',
    data() {
        return {
            currentNum: '',
            prevNum: ''
        }
    },
    methods: {
        addNum(num) {
            this.currentNum = this.currentNum.toString() + num.toString();
        },
        addInt(int) {
            this.prevNum = this.currentNum.toString() + int.toString();
            this.currentNum = '';
        },
        calc() {
            const nok = this.prevNum.toString() + this.currentNum.toString();
            this.currentNum = eval(nok).toString();
            this.prevNum = '';
        },
        clear() {
            this.currentNum = '';
            this.prevNum = '';
        }
    }
}
</script>
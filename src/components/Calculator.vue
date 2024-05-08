<template>
    <div id="app">
        <div id="calculator">
            <div class="calculator-screen p-2 fs-2" id="result" :value="displayOnScreen" disabled>{{  showAnswer ? answer : displayOnScreen  }}</div>
            <div class="calculator-keys">
                <div class="row">
                    <div class="col-8 p-0">
                        <button v-for="(op, index) in operators.slice(0, 3)" @click="handleOperation" type="button"
                            :value="op" :key="index" class="operator btn btn-success">{{ op }}</button>
                    </div>
                    <div class="col-4 p-0">
                        <button v-for="(op, index) in operators.slice(3,)" @click="handleOperation" type="button" :value="op"
                            :key="index" class="operator btn btn-success">÷</button>
                    </div>
                </div>


                <div class="row">
                    <div class="col-8 p-0 ">
                        <button type="button" @click="handleNumber" class="number btn btn-light" :value="n"
                            v-for='(n, index) in keys' :key="index">{{ n }} </button>
                        <button type="button"  @click="handleNumber" id="decimal" value="." class="number btn btn-light">.</button>
                        <button @click="clear" type="button" id="clear" value="all-clear"
                            class="all-clear number btn btn-danger">AC</button>
                    </div>
                    <div class="col-4 p-0">
                        <button @click="handleEquals" type="button" id="equals" class="number equal-sign btn btn-light">=</button>
                    </div>
                </div>

            </div>
        </div>
    </div>
</template>
  



<script>


export default {
    name: 'Calculator',
    data: function () {
        return {
            keys: [7, 8, 9, 4, 5, 6, 1, 2, 3, 0],
            operators: ['+', '-', '*', '/'],
            currentInput: '',
            answer: '',
            showAnswer: false,
            operation: '',
            operand: ''

        }
    },
    computed: {
        displayOnScreen: function () {
            if (this.showAnswer) {
                return this.answer
            }
            else {
                return `${this.operand} ${this.operation} ${this.currentInput} `;
            }
        }
    },
    methods: {
        handleNumber: function (event) {
            if (this.showAnswer) {
                this.showAnswer = false;
            }
            this.currentInput += event.target.value
            

        },
        handleOperation: function (event) {
            if(this.showAnswer){
                this.operand = this.answer;
                this.showAnswer=false;   
            }
            else{
                this.operand = this.currentInput;
            }
            this.operation = event.target.value;
            this.currentInput = '';
        },
        calculate: function (o1, op, o2) {

            switch (op) {
                case '+':
                    return parseFloat(o1) + parseFloat(o2)

                case '-':
                    return parseFloat(o1) - parseFloat(o2)

                case '*':
                    return parseFloat(o1) * parseFloat(o2)

                case '/':
                    return parseFloat(o1) / parseFloat(o2)
            }
        },

        handleEquals: function(){   
            if(this.currentInput === ''){
                this.currentInput = '0';
            }
            this.answer = this.calculate(this.operand,this.operation,this.currentInput);
            this.operation='';
            this.currentInput='';
            this.showAnswer=true;
        },

        clear: function(){
            this.currentInput=''
            this.answer=''
            this.operand=''
            this.operation=''
            this.showAnswer=false
        }
    }
}
</script>
  
<style>
#calculator {
    margin: auto;
    width: 30%;
    background-color: darkslategray;
    padding: 10px;

}


.calculator-keys {
    width: 408px;
    margin: 20px;
}

.calculator-screen {
    background-color: black;
    color: white;
    font-weight: 700;
    width: 408px;
    height: 70px;
}

.operator {
    width: 92px;
    height: 70px;
    margin-right: 2px;
    padding: 0px;
    font-weight: bolder;
    font-size: 50px;
    margin-top: 10px;

}

.number {
    width: 92px;
    height: 70px;
    margin: 1px;
    font-weight: bolder;
    font-size: 50px;
    margin-top: 10px;

}

.col {
    width: 100%;
    margin: auto;
    grid-gap: 0px
}

#equals {
    height: 310px;
}
</style>
  
<template>
  <div>
    <input readonly type="text" :value=this.calculatorText size="20">
    <button v-on:click="calculate()" :disabled=this.disabledCalculate>=</button>
    <br>
    <button v-on:click="onClickNumber('7')" :disabled=this.disabledNumbers>7</button>
    <button v-on:click="onClickNumber('8')" :disabled=this.disabledNumbers>8</button>
    <button v-on:click="onClickNumber('9')" :disabled=this.disabledNumbers>9</button>
    <button v-on:click="onClickOperator('/')" :disabled=this.disabledOperators>÷</button>
    <br>
    <button v-on:click="onClickNumber('4')" :disabled=this.disabledNumbers>4</button>
    <button v-on:click="onClickNumber('5')" :disabled=this.disabledNumbers>5</button>
    <button v-on:click="onClickNumber('6')" :disabled=this.disabledNumbers>6</button>
    <button v-on:click="onClickOperator('x')" :disabled=this.disabledOperators>x</button>
    <br>
    <button v-on:click="onClickNumber('1')" :disabled=this.disabledNumbers>1</button>
    <button v-on:click="onClickNumber('2')" :disabled=this.disabledNumbers>2</button>
    <button v-on:click="onClickNumber('3')" :disabled=this.disabledNumbers>3</button>
    <button v-on:click="onClickOperator('-')" :disabled=this.disabledOperators>-</button>
    <br>
    <button v-on:click="onClickNumber('0')" :disabled=this.disabledNumbers>0</button>
    <button v-on:click="onClickNumber('.')" :disabled=this.disabledNumbers>.</button>
    <button v-on:click="reset()">C</button>
    <button v-on:click="onClickOperator('+')" :disabled=this.disabledOperators>+</button>
    <br>
  </div>
</template>
  
<script>
export default {
  name: 'CalculatorMain',
  data() {
    return {
      calculatorText: '',
      calculatorValue: '',
      operator: '',
      currentFirstPart: '',
      disabledNumbers: false,
      disabledOperators: true,
      disabledCalculate: false
    }
  },
  methods: {
    onClickNumber  (number) {
      // clicking an number
      this.calculatorValue = this.calculatorValue + number.toString()
      this.calculatorText = this.calculatorText + number.toString()
      this.disabledCalculate = false

      if (this.calculatorValue.length > 0 && this.currentFirstPart.length === 0) {
        this.disabledOperators = false
      }
    },
    onClickOperator (operator) {
      // clicking an operator - disable operators because only two two number operation allowed
      this.currentFirstPart = this.calculatorText
      this.operator = operator
      this.calculatorText = this.calculatorText + operator
      this.calculatorValue = ''
      this.disabledOperators = true
      this.disabledCalculate = false
    },
    reset () {
      // reset all as initial
      this.calculatorText = ''
      this.calculatorValue = ''
      this.currentFirstPart = ''
      this.currentSecondPart = ''
      this.operator = ''
      this.disabledNumbers = false
      this.disabledOperators = true
      this.disabledCalculate = false
    },
    calculate () {
      // switch-case to operate four possibilities
      switch (this.operator) {
        case "x":
          this.calculatorText = Number(this.currentFirstPart) * Number(this.calculatorValue)
          break;
        case "/":
          this.calculatorText = Number(this.currentFirstPart) / Number(this.calculatorValue)
          break;
        case "+":
          this.calculatorText = Number(this.currentFirstPart) + Number(this.calculatorValue)
          break;
        case "-":
          this.calculatorText = Number(this.currentFirstPart) - Number(this.calculatorValue)
          break;
        default:
          break;
      }
      // error control - not a number and empty second part (syntax error)
      if (this.calculatorText.toString() === 'NaN' || this.calculatorValue.toString() === '') {
        this.calculatorText = 'Syntax Error'
        this.disabledOperators = true
        this.disabledNumbers = true
        this.disabledCalculate = true
      } else {
        this.currentFirstPart = this.calculatorText
        this.calculatorValue = ''
        this.disabledOperators = false
        this.disabledCalculate = true
      }
    }
  }
}
</script>
  
<style>
  input {
    background-color: #cecece;
    border: 2px solid #000000;
    border-radius: 10px;
    color: black;
    padding: 15px 83px;
    margin: 10px;
    text-align: right;
    font-size: 16px;
  }
  button {
    background-color: #00c85d;
    border: 2px solid #000000;
    border-radius: 10px;
    color: rgb(255, 255, 255);
    padding: 15px 32px;
    margin: 10px;
    text-align: center;
    font-size: 16px;
  }
  button:disabled,
  button[disabled]{
    border: 2px solid #999999;
    border-radius: 10px;
    background-color: #cccccc;
    color: rgb(255, 255, 255);
    padding: 15px 32px;
    margin: 10px;
    text-align: center;
    font-size: 16px;
  }
</style>
  
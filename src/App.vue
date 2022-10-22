<template>
  <div id="app">
    <div class="container">
      <div class = 'fields'>
        <div class="operands">
          <input v-bind:class="{active:activeOperand == 1}" @click= "activateOperand(1)" ref = "input1" type = 'number' v-model = 'operand1'/>
          <span> {{currentOperation}}</span>
          <input v-bind:class="{active:activeOperand == 2}" @click= "activateOperand(2)" ref = "input2" type = 'number' v-model = 'operand2'/>
          <div v-show = "show"> = {{calculate(currentOperation)}} </div>
        </div>
        
        <div class = 'keys'>
            <button v-for = "item, index of operations" 
              v-bind:key = "index" 
              @click = "currentOperation = item">
              {{item}}
            </button>

        </div>
        <div v-show = "error" class="error">{{ error }}</div>
      </div>
      
      <div class="keyboard">
        <label>
          <input @change = "showKeyboard" type="checkbox" /> Отобразить экранную клавиатуру
        </label>
        
        <div v-show = "checked" class="keys">
          <button v-for = "item of keys" v-bind:key="item" @click="getNumber(item)">
            {{item}}
          </button>
          <button @click="deleteNumber"> &lt;= </button>
        </div>

        <div v-show = "checked" class="operand-inputs">
          <label>
            <input v-bind:checked="activeOperand == 1" ref = "oper1" name = inputs type="radio" @change = "activateOperand(1)"> Операнд 1
          </label>
          <label>
            <input v-bind:checked="activeOperand == 2" ref = "oper2" name = inputs type="radio" @change = "activateOperand(2)"> Операнд 2
          </label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      operand1: 0,
      operand2: 0,
      currentOperation: '+',
      error: '',
      show: false,
      operations: ['+', '-', '*', '/', 'pow', '%'],
      keys: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'],
      activeOperand: 1,
      checked: false
    }
  },
  computed: {
    result() { 
      return this.calculate(this.currentOperation);
    },
  },
 
  methods: {
    showKeyboard() {
      this.checked = !this.checked;
    },
   
    activateOperand(id) {
      this.activeOperand = id;
    },

    getNumber(num) {
      if (this.activeOperand == 1) {
        if (this.operand1 == 0) this.operand1 = '';
        this.operand1 = this.operand1 + num;
      } else {
        if (this.operand2 == 0) this.operand2 = '';
        this.operand2 = this.operand2 + num;
      }
    },

    deleteNumber() {
      if (this.activeOperand == 1) {
        this.operand1 = Math.floor(+this.operand1 / 10);
      } else {
        this.operand2 = Math.floor(this.operand2 / 10);
      }
    },

    sum() {
        return +this.operand1 + +this.operand2;
    },

    minus() {
        return this.operand1 - this.operand2;
    },

    mult() {
        return this.operand1 * this.operand2;
    },

    divide() {
      if (this.operand2 == 0) {
        this.error = 'На ноль делить нельзя!';
        this.show = false;
      } else {
        return this.operand1 / this.operand2;
      }
    },

    pow() {
        return this.operand1 ** this.operand2;
    },

    division() {
      if (+this.operand2 == 0) {
        this.error = 'На ноль делить нельзя!';
        this.show = false;
      } else {
        return this.operand1 % this.operand2;
      }
    },
    calculate(operation = '+')  {
      this.error = '';
      this.show = true;
      switch (operation) {
        case "+":
          return this.sum();
        case "-":
          return this.minus();
        case "*":
          return this.mult();
        case "/":
          return this.divide();
        case "pow":
          return this.pow();
        case "%":
          return this.division();
      }
      
  }
}
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container {
  margin: 0 auto;
  width: 1200px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.fields {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 30px;
}
.operands {
  width: 400px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.operands input {
  width: 100px;
  outline: none;
}
.operands p {
  font-size: 20px;
  margin: 0;
  padding: 0;
}
.keyboard {
  display: flex;
  flex-direction: column;
}
.keys {
  display: flex;
}
.keys button {
  width: 20px;
  height: 20px;
}
.keys {
  margin: 10px;
  display: flex;
}
.keys button{
    width: 35px;
}
.operand-inputs {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}
.error {
  margin: 10px 0;
  color: red;
  border: 2px solid red;
  display: block;
  padding: 10px 20px;
}
.active {
  border: 1px solid blue;
}
</style>

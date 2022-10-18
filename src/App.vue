<template>
  <div id="app">
    <div class = 'operands'>
      <input type = 'number' v-model = 'operand1'/>
          <div class = 'keys'>
            <button v-on:click = "result = +operand1 + +operand2 ">+</button>
            <button @click = "result = +operand1 - +operand2 ">-</button>
            <button @click = "result = +operand1 * +operand2 ">*</button>
            <button @click = "result = +operand1 / +operand2 ">/</button>
            <button @click = "result = (+operand1) ** (+operand2) ">pow</button>
            <button @click = "result = +operand1 % +operand2 ">%</button>
          </div>
      <input type = 'number' v-model = 'operand2'/>
      <p> = </p>
      <p> {{result}} </p>
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
      result: 0
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
.operands {
  width: 400px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.operands input {
  width: 50px;
  margin-left: 10px;
}
.operands p {
  font-size: 20px;
  margin: 0;
  padding: 0;
}
.keys {
  margin: 10px;
  display: flex;
}
.keys button{
    width: 35px;
}
</style>

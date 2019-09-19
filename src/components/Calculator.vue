<template>
  <div class="calculator">
    <span class="result"> {{current || '0'}} </span>
    <span @click="append('7')" class ="btn">7 </span>
    <span @click="append('8')" class ="btn">8 </span>
    <span @click="append('9')" class ="btn">9 </span>
    <span @click="add" class ="btn">+ </span>
    <span @click="append('4')" class ="btn">4 </span>
    <span @click="append('5')" class ="btn">5 </span>
    <span @click="append('6')" class ="btn">6 </span>
    <span @click="subtract" class ="btn">- </span>
    <span @click="append('1')" class ="btn">1 </span>
    <span @click="append('2')" class ="btn">2 </span>
    <span @click="append('3')" class ="btn">3 </span>
    <span @click="multiply" class ="btn">* </span>
    <span @click ='clear' class ="btn">C </span>
    <span @click="append('0')" class ="btn">0 </span>
    <span @click="divide" class ="btn">/ </span>
    <span @click="equal" class ="btn">= </span>
  </div>
</template>

<script>
import { METHODS } from 'http'
export default {
  data(){
    return{
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear(){
      this.current = '';
    },
    append(number){
      if(this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    helper(){
      this.previous = this.current;
      this.operatorClicked = true;
    },
    add(){
      this.operator = (a, b) => a + b;
      this.helper();
    },
    subtract(){
      this.operator = (a, b) => a - b;
      this.helper();
    },
    multiply(){
      this.operator = (a, b) => a * b;
      this.helper();
    },
    divide(){
      this.operator = (a, b) => a / b;
      this.helper();
    },
    equal(){
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  border: 1px solid #333;
  text-align: right;
  margin: 0 auto;
  width: 400px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50üx, auto);
}

.result {
  grid-column: 1 / 5;
}

.btn{
  text-align: center;
  background-color: aliceblue;
  border: 1px solid #333;
}
</style>

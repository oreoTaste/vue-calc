<template>
  <div id="app">
    <div class="calculator">
      <div class="result">{{curNote}}</div>
      <div class="btn-ac" v-on:click="clear">AC</div>
      <div class="btn-plsmns" v-on:click="changePlsMns">+/-</div>
      <div class="btn-del" v-on:click="deleteDigit">DEL</div>
      <div class="btn-div" v-on:click="onClickDevide">/</div>
      <div class="btn-num" v-on:click="onClickNum">7</div>
      <div class="btn-num" v-on:click="onClickNum">8</div>
      <div class="btn-num" v-on:click="onClickNum">9</div>
      <div class="btn-mul" v-on:click="onClickMultiply">x</div>
      <div class="btn-num" v-on:click="onClickNum">4</div>
      <div class="btn-num" v-on:click="onClickNum">5</div>
      <div class="btn-num" v-on:click="onClickNum">6</div>
      <div class="btn-min" v-on:click="onClickMinus">-</div>
      <div class="btn-num" v-on:click="onClickNum">1</div>
      <div class="btn-num" v-on:click="onClickNum">2</div>
      <div class="btn-num" v-on:click="onClickNum">3</div>
      <div class="btn-pls" v-on:click="onClickPlus">+</div>
      <div class="btn-num btn-zero" v-on:click="onClickNum">0</div>
      <div class="btn-dot" v-on:click="onClickDot">.</div>
      <div class="btn-equ" v-on:click="onClickEqual">=</div>
    </div>
  </div>
</template>

<script>
  const calc = (text) => {
    return eval(text);
    // let operand = text.split(/[+-/*]/);
    // let operation = text.split('').filter(el => el == '+' || el == '-' || el == '*' || el == '/');
    // console.log(operand);
    // console.log(operation);
    // operation.forEach((el, ind, arr) => if(el == '*' || el == '/') 
    // )
  }

  const slice = (num) => {
    let tmp = num + '';
    if(tmp.length <= 1) {
      return null;
    }
    return tmp.split('').filter((el, ind, arr) => ind < arr.length-1).join('');
  }
export default {
  data(){
    return {
      curStatus: false,
      curNote: 0,
      opStatus: false,
    }
  },
  methods: {
    clear(){
      this.curStatus = false;
      this.curNote = 0;
    },
    
    changePlsMns(){
      if(this.curStatus == true && this.opStatus == false) {
        this.curNote = -this.curNote;
      }
    },

    deleteDigit(){
      if(this.curStatus == true && this.opStatus == false) {
        this.curNote = slice(this.curNote) ? slice(this.curNote) : 0;
      }
    },

    onClickNum: function(e) {
      this.curStatus = true;
      if(this.curNote == 0) {
        this.curNote = e.target.innerText;
      } else {
        this.curNote += e.target.innerText;
      }
    },

    onClickDot() {
      this.curStatus = true;
      if(this.curNote.indexOf('.') < 0) {
        this.curNote += '.'; 
      }
    },

    onClickPlus() {
      if(this.curStatus == true) {
        this.curNote += '+';
        this.opStatus = true;
      }      
    },
    onClickMinus() {
      if(this.curStatus == true) {
        this.curNote += '-';
        this.opStatus = true;
      }
    },
    onClickMultiply() {
      if(this.curStatus == true) {
        this.curNote += '*';
        this.opStatus = true;
      }
    },
    onClickDevide() {
      if(this.curStatus == true) {
        this.curNote += '/';
        this.opStatus = true;
      }
    },

    onClickEqual() {
      if(this.opStatus == false) {
        return;
      }
    
      this.curNote = calc(this.curNote);
      this.opStatus = false;
    },
  
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: black;
  margin: 3rem;
}
.calculator {
  display: grid;
  grid-template: repeat(1fr, 5) / repeat(1fr, 4);
}
.calculator > * {
  border: 1px solid black;
  height: 3rem;
  line-height: 3rem;
  color: white;
}
.calculator > *:not(.result) {
  cursor: pointer;
  user-select: none;
}
.result {
  grid-column: 1 / span 4;
  grid-row: 1 / span 1;
}
.btn-zero {
  grid-column: 1 / span 2;
  grid-row: 6 / span 1;
}
.btn-ac,
.btn-plsmns,
.btn-del {
  background-color: #F2F2F2;
  color: black;
}
.btn-num,
.btn-dot {
  background-color: gray;  
}
.btn-div,
.btn-mul,
.btn-min,
.btn-pls,
.btn-equ {
  background-color: orange;
}

</style>

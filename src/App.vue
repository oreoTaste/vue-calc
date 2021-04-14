<template>
  <div id="app">
    <div class="calculator">
      <div class="result">{{curNote}}</div>
      <div class="btn btn-ac btn-white" v-on:click="clear">AC</div>
      <div class="btn btn-plsmns btn-white" v-on:click="changePlsMns">+/-</div>
      <div class="btn btn-del btn-white" v-on:click="deleteDigit">DEL</div>
      <div class="btn btn-div btn-orange" v-on:click="onClickDevide">/</div>
      <div class="btn btn-num" v-on:click="onClickNum">7</div>
      <div class="btn btn-num" v-on:click="onClickNum">8</div>
      <div class="btn btn-num" v-on:click="onClickNum">9</div>
      <div class="btn btn-mul btn-orange" v-on:click="onClickMultiply">x</div>
      <div class="btn btn-num" v-on:click="onClickNum">4</div>
      <div class="btn btn-num" v-on:click="onClickNum">5</div>
      <div class="btn btn-num" v-on:click="onClickNum">6</div>
      <div class="btn btn-min btn-orange" v-on:click="onClickMinus">-</div>
      <div class="btn btn-num" v-on:click="onClickNum">1</div>
      <div class="btn btn-num" v-on:click="onClickNum">2</div>
      <div class="btn btn-num" v-on:click="onClickNum">3</div>
      <div class="btn btn-pls btn-orange" v-on:click="onClickPlus">+</div>
      <div class="btn btn-num btn-zero" v-on:click="onClickNum">0</div>
      <div class="btn btn-dot" v-on:click="onClickDot">.</div>
      <div class="btn btn-equ btn-orange" v-on:click="onClickEqual">=</div>
    </div>
  </div>
</template>

<script>

  const calc = (text) => {
    return eval(text);
    // let operand = text.split(/[+-/*]/);
    // let operation = text.split('').filter(el => el == '+' || el == '-' || el == '*' || el == '/');
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
      opCheck: false,
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
      this.opCheck = false;
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
      if(this.opCheck) { // 연산자 중복입력 불가 체크 및 부호 변경가능 기능 추가
        this.curNote = this.curNote.slice(0, this.curNote.length - 1) + '+';
      }
      if(this.curStatus == true && !this.opCheck) {
        this.curNote += '+';
        this.opStatus = true;
        this.opCheck = true;
      }      
    },
    onClickMinus() {
      if(this.opCheck) {
        this.curNote = this.curNote.slice(0, this.curNote.length - 1) + '-';
      }
      if(this.curStatus == true && !this.opCheck) {
        this.curNote += '-';
        this.opStatus = true;
        this.opCheck = true;
      }
    },
    onClickMultiply() {
      if(this.opCheck) {
        this.curNote = this.curNote.slice(0, this.curNote.length - 1) + '*';
      }
      if(this.curStatus == true && !this.opCheck) {
        this.curNote += '*';
        this.opStatus = true;
        this.opCheck = true;
      }
    },
    onClickDevide() {
      if(this.opCheck) {
        this.curNote = this.curNote.slice(0, this.curNote.length - 1) + '/';
      }
      if(this.curStatus == true && !this.opCheck) {
        this.curNote += '/';
        this.opStatus = true;
        this.opCheck = true;
      }
    },

    onClickEqual() {
      if(this.opStatus == false) {
        return;
      }
      if(this.opCheck) {
        this.curNote = this.curNote.slice(0, this.curNote.length - 1);
      }
    
      this.curNote = calc(this.curNote);
      this.opStatus = false;
      this.opCheck = false;
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
  grid-template: repeat(1fr, 6) / repeat(1fr, 4);
}
.calculator > * {
  border: 1px solid black;
  height: 3rem;
  line-height: 3rem;
  color: white;
}
.btn {
  cursor: pointer;
  user-select: none;
  background-color: gray;  
}
.btn-white {
  background-color: #F2F2F2;
  color: black;
}
.btn-orange {
  background-color: orange;
}
.result {
  grid-column: 1 / span 4;
  grid-row: 1 / span 1;
  text-align: right;
  padding-right: 2.5rem;
}
.btn-zero {
  grid-column: 1 / span 2;
  grid-row: 6 / span 1;
}


</style>

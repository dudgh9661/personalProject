<template>
  <html lang="en">
  <head>
    <link rel="stylesheet" type="text/css" href="./index.css" />
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <!-- <script src="https://cdn.jsdelivr.net/npm/vue@2.6.0"></script>     -->
    <!-- <script src="./calculator.js"></script> -->
    <title>계산기</title>
  </head>
  <body>
    <div id="container">
      <div>
        <div>
          <input type="hidden" v-model="input"/>
        </div>
        <div>
          <input id="resultPage" type="text" v-model="result"/>
        </div>
 
        <div>
          <div class="buttonWrap">
            <button v-on:click="reset()">AC</button>
            <button v-on:click="changeOperator()">+/-</button>
            <button v-on:click="del()">DEL</button>
            <button id="operator" v-on:click="addOutput('/')">/</button>
          </div>
          <div class="buttonWrap">
            <button id="number"  v-on:click="addOutput(7)">7</button>
            <button id="number"  v-on:click="addOutput(8)">8</button>
            <button id="number"  v-on:click="addOutput(9)">9</button>
            <button id="operator"  v-on:click="addOutput('*')">*</button>
          </div>
          <div class="buttonWrap">
            <button id="number"  v-on:click="addOutput(4)">4</button>
            <button id="number"  v-on:click="addOutput(5)">5</button>
            <button id="number"  v-on:click="addOutput(6)">6</button>
            <button id="operator"  v-on:click="addOutput('-')">-</button>
          </div>
          <div class="buttonWrap">
            <button id="number" v-on:click="addOutput(1)">1</button>
            <button id="number" v-on:click="addOutput(2)">2</button>
            <button id="number" v-on:click="addOutput(3)">3</button>
            <button id="operator"  v-on:click="addOutput('+')">+</button>
          </div>
          <div class="buttonWrap">
            <button id="number" style="width:260px" v-on:click="addOutput(0)">0</button>
            <button id="number" v-on:click="addOutput('.')">.</button>
            <button id="operator"  v-on:click="Calculate()">=</button>
          </div>
        </div>
      </div>
    </div>
    
  </body>
</html>
</template>

<script>
export default {
  data() {
    return {
      input : "0",
      result : "0",
      needZero : true
    }
  },
  methods: {
    addOutput(num) {
      if( this.needZero ) {
        this.result = "";
        this.input = "";
        this.needZero = false;
      }
       this.result = this.result + num;
       this.input = this.input + num;
    },
    Calculate() {
      var answer = eval(this.result);
      this.result = answer;
      this.input = answer;
    },
    del() {
      if( this.input.length == 1 ) {
        this.input = "0";
        this.result = "0";
        this.needZero = true;
      }
      else {
        this.input = this.input.substring(0, this.input.length - 1);
        this.result = this.input;
      }
    },
    reset() {
      this.needZero = true;
      this.input = "0";
      this.result = "0";
    },
    changeOperator() {
      var change = this.input;

      if (!isNaN(change) && change.length != 0) {
          if (change[0] !== '-') change = '-' + change;
          else if (change[0] === '-') { //부호가 -이면
              change = change.substring(1, change.length);
          }
      }

      this.input = change;
      this.result = change;
    }

  }
}
</script>

<style>
#container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%; 
}
 
#container > div {
  
  border: 2px solid black;
}
 
#displayPage,
#resultPage {
  width: 505px;
  height: 80px;
  font-size: 60px;
  font-weight: bold;
  color: white;
  background-color: black;
  text-align: right;
  padding-right: 8px;
  border: 2px solid black;
}
 
.buttonWrap {
  display: flex;
  flex-direction: col;
}
 
.buttonWrap button {
  width: 129px;
  height: 50px;
  font-size: 20px;
  padding: 10px;
}

.buttonWrap button:hover {
  background-color: #d2d2d2;
}

.buttonWrap button:active {
  background-color: #dcdcdc;
}


.buttonWrap #number {
  background-color: #5a5a5a;
  color: white;
}

.buttonWrap #number:hover {
  background-color: #a0a0a0;
}

.buttonWrap #number:active {
  background-color: #bebebe;
}

.buttonWrap #operator {
  background-color: #DB631F	;
  color: white;
}

.buttonWrap #operator:hover {
  background-color: #E56D29;
}

.buttonWrap #operator:active {
  background-color: #F49551;
}


</style>

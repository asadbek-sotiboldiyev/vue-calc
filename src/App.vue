<template>
  <div id="calc">
    <h1 class="main-title"><span>VueJs</span> calc</h1>
    <div class="panel">
      <p class="memory">{{ memory }}</p>
      <div class="result-panel">
        <h1 class="command">{{ command }}</h1>
        <h1 class="result">{{ result }}</h1>
      </div>
    </div>
    <div class="btns-panel panel">
      <div class="btn-group">
        <button class="btn" @click="numberHandler(7)">7</button>
        <button class="btn" @click="numberHandler(8)">8</button>
        <button class="btn" @click="numberHandler(9)">9</button>
        <button class="btn btn-dark" @click="del">DEL</button>
      </div>
      <div class="btn-group">
        <button class="btn" @click="numberHandler(4)">4</button>
        <button class="btn" @click="numberHandler(5)">5</button>
        <button class="btn" @click="numberHandler(6)">6</button>
        <button class="btn" @click="commandHandler('+')">+</button>
      </div>
      <div class="btn-group">
        <button class="btn" @click="numberHandler(1)">1</button>
        <button class="btn" @click="numberHandler(2)">2</button>
        <button class="btn" @click="numberHandler(3)">3</button>
        <button class="btn" @click="commandHandler('-')">-</button>
      </div>
      <div class="btn-group">
        <button class="btn" @click="dot">.</button>
        <button class="btn" @click="numberHandler(0)">0</button>
        <button class="btn" @click="commandHandler('/')">/</button>
        <button class="btn" @click="commandHandler('*')">*</button>
      </div>
      <div class="btn-group">
        <button class="btn btn-dark btn-block" @click="clearAll">CLEAR</button>
        <button class="btn btn-red btn-block" @click="equal">=</button>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      result: '0',
      command: '',
      memory: 0
    }
  },

  methods: {
    numberHandler(number) {
      if (this.result == '0' || this.result == 'Infinity')
        this.result = '';
      if (this.result.length >= 13)
        return;
      this.result += `${number}`
    },
    commandHandler(command) {
      if(this.result == 'Infinity')
        this.result = '0';
      if (this.command === '') {
        this.memory = this.result;
        this.command = command;
        this.result = 0;
      }else{
        var s = this.memory + this.command + this.result;
        var d = eval(s);
        if(d == 'Infinity' || isNaN(d))
          d = 0;
        this.command = command;
        this.memory = d;
        this.result = 0;
      }
    },
    equal(){
      if(this.command === '') return;
      var d = eval(this.memory + this.command + this.result);
      d = d.toString().substring(0, 13);
      if(isNaN(d) || d == 'Infinity')
        d = 0;
      this.result = d;
      this.memory = 0;
      this.command = '';
    },
    del(){
      this.result = this.result.toString();
      if(this.result == 'Infinity' || isNaN(this.result))
        this.result = '0';
      if(this.result.length <= 1)
        this.result = '0';
      else{
        var sub = this.result.substring(0, this.result.length-1);
        this.result = sub;
      }
    },
    dot(){
      if(this.result.includes('.')) return;
      this.result += '.';
    },
    clearAll() {
      this.memory = 0;
      this.result = '0';
      this.command = '';
    }
  }

}
</script>

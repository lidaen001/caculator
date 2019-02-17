<template>
  <div class="caculator">
    <div class="display">{{current||"0"}}</div>
    <div v-on:click="clear()" class="btn">C</div>
    <div v-on:click="sign()" class="btn">+/-</div>
    <div v-on:click="percent()" class="btn">%</div>
    <div v-on:click="divide()" class="btn operator">÷</div>
    <div v-on:click="append('7')" class="btn">7</div>
    <div v-on:click="append('8')" class="btn">8</div>
    <div v-on:click="append('9')" class="btn">9</div>
    <div v-on:click="times()" class="btn operator">×</div>
    <div v-on:click="append('4')" class="btn">4</div>
    <div v-on:click="append('5')" class="btn">5</div>
    <div v-on:click="append('6')" class="btn">6</div>
    <div v-on:click="minus()" class="btn operator">-</div>
    <div v-on:click="append('1')" class="btn">1</div>
    <div v-on:click="append('2')" class="btn">2</div>
    <div v-on:click="append('3')" class="btn">3</div>
    <div v-on:click="plus()" class="btn operator">+</div>
    <div v-on:click="append('0')" class="btn zero">0</div>
    <div v-on:click="dot()" class="btn">.</div>
    <div v-on:click="equals()" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      current:'',
      previous: '',
      operator: null,
      operatorClicked: false
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"? 
          this.current.slice(1)
          : "-" + this.current;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current + number}`;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
      // this.current="";
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equals(){
      this.current=`${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
        )}`;
        this.previous='';
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.caculator {
  width: 400px;
  margin: 0 auto;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display {
  grid-column: 1/5;
  background-color: #333;
  color: white;
}
.zero {
  grid-column: 1/3;
}
.btn {
  background-color: #eee;
  border: 1px solid #999;
}
.operator {
  background-color: orange;
}
</style>

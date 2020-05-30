<template>
  <div class="calculator">
    <div class="display">{{current || 0}}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiply" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="plus" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equals" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: "",
      operator: null,
      clickedOperator: false,
    }
  },

  methods: {

    clear() {
      this.current = "";
    },

    sign() {
      this.current = this.current.charAt(0) == '-' ?
        this.current.slice(1) : `-${this.current}` ;
    },

    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },

    append(number) {
      if (this.clickedOperator) {
        this.current = "";
        this.clickedOperator = false;
      }
      this.current = `${this.current}${number}`;
    },

    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },

    setPrevious() {
      this.previous = this.current;
      this.clickedOperator = true;
    },

    divide(){
      this.operator = (a, b) => (b / a);
      this.setPrevious();
    },

    multiply() {
      this.operator = (a, b) => (a * b);
      this.setPrevious();
    },

    minus() { 
      this.operator = (a, b) => (b - a);
      this.setPrevious();
    },

    plus() { 
      this.operator = (a, b) => (a + b);
      this.setPrevious();
    },

   equals() {
      this.current = `${this.operator(
        parseFloat(this.current), 
        parseFloat(this.previous)
        )}`;
        this.previous = null;
      },

  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .calculator {
    margin: 0 auto;
    width: 400px;
    font-size: 40px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
  }

  .display {
    grid-column: 1/5;
    background-color: #ff7c47;
    color: white;
    border: 2px solid #ff692e ;
    text-align: right;
    padding: 2px;
    padding-right: 5px;
  }

  .zero {
    grid-column: 1/3;
  }

  .btn {
    background-color: #ffd7c7;
    border: 1px solid #ff692e;
    color: darkslategrey;
    cursor:pointer
  }

  .btn:active {
   transform: scale(0.95);
  }

  .operator {
    background-color: #ffa07a;
    color: white;
  }



</style>

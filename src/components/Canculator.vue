<template>
  <div class="body">
    <div class="canculator">
      <div class="display">
        <span class="display__item">{{ current || '0' }}</span>
      </div>
      <div @click="clear" class="orange">
        <span>C</span>
      </div>
      <div @click="sign" class="orange">
        <span>+/-</span>
      </div>
      <div @click="percent" class="orange">
        <span>%</span>
      </div>
      <div @click="divide" class="orange">
        <span>÷</span>
      </div>
      <div @click="append('7')" class="number">
        <span>7</span>
      </div>
      <div @click="append('8')" class="number">
        <span>8</span>
      </div>
      <div @click="append('9')" class="number">
        <span>9</span>
      </div>
      <div @click="times" class="orange">
        <span>×</span>
      </div>
      <div @click="append('4')" class="number">
        <span>4</span>
      </div>
      <div @click="append('5')" class="number">
        <span>5</span>
      </div>
      <div @click="append('6')" class="number">
        <span>6</span>
      </div>
      <div @click="minus" class="orange minus">
        <span>—</span>
      </div>
      <div @click="append('1')" class="number">
        <span>1</span>
      </div>
      <div @click="append('2')" class="number">
        <span>2</span>
      </div>
      <div @click="append('3')" class="number">
        <span>3</span>
      </div>
      <div @click="add" class="orange">
        <span>+</span>
      </div>
      <div></div>
      <div @click="append('0')" class="number">
        <span>0</span>
      </div>
      <div @click="dot" class="point number">
        <span>,</span>
      </div>
      <div @click="equal" class="orange">
        <span>=</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Canculator',
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = ''
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ?
        this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`
      this.setPrevious()
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = ''
        this.operatorClicked = false
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.')
      }
    },
    setPrevious() {
      this.previous = this.current
      this.operatorClicked = true
    },
    divide() {
      this.operator = (a, b) => a / b
      this.setPrevious()
    },
    times() {
      this.operator = (a, b) => a * b
      this.setPrevious()
    },
    minus() {
      this.operator = (a, b) => a - b
      this.setPrevious()
    },
    add() {
      this.operator = (a, b) => a + b
      this.setPrevious()
    },
    equal() {
      this.current = `${
        this.operator(
          parseFloat(this.current),
          parseFloat(this.previous)
        )}`
      this.previous = null
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.canculator {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  max-width: 500px;
  margin: 0 auto;
  height: 100vh;
}
.canculator > div > span {
  cursor: pointer;
}
.display {
  grid-column: 1 / 5;
  border-bottom: 1px solid #b7b7b7;
  height: 200px;
  color: #ffffff;
  font-size: 40px;
  display: flex;
  justify-content: end;
  align-items: end;
}
.display__item {
  margin: 0 10px 10px 0;
}
.orange {
  color: #cc7001;
  font-weight: bold;
  font-size: 25px;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 70px !important;
  height: 70px !important;
}
span {
  font-weight: bold;
}
.point > span {
  font-size: 20px;
}
.body {
  background-color: #262626;
  padding: 10px;
  width: 100%;
  margin: auto;
  height: 100vh;
  overflow: hidden;
}
.number {
  color: #fff;
  font-size: 30px;
  display: flex;
  align-items: start;
  justify-content: center;
}
.number > span {
  border: 1px solid gray;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 70px;
  height: 70px;
  border-radius: 12px;
  background-color: #484848;
}
.minus {
  font-size: 20px;
}
</style>

<template>
  <div class="calculator">
    <div class="wrapper">
      <div class="result">{{ currentEquation }}</div>
      <div class="calculation">
        <div class="numbers">
          <button
            class="number"
            v-for="number in numbers"
            :key="number"
            @click="calculate(number)"
          >
            {{ number }}
          </button>
        </div>
        <div class="operators">
          <button
            class="button"
            v-for="button in buttons"
            :key="button"
            @click="calculate(button)"
          >
            {{ button }}
          </button>
        </div>
      </div>
      <div class="equation">
        <button @click="calculate('=')">=</button>
        <button @click="showHistory">History</button>
      </div>

      <div v-show="showingHistory" class="history">
        <h3>Equation History</h3>
        <ul>
          <li v-for="equation in equationHistory" :key="equation">
            {{ equation }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      result: 0,
      numbers: ['7', '8', '9', '4', '5', '6', '1', '2', '3', '0', 'AC', '.'],
      buttons: ['/', '*', '+', '-'],
      equationHistory: [],
      showingHistory: false,
      currentEquation: '',
    };
  },
  methods: {
    calculate(button) {
      if (button === '=') {
        this.result = eval(this.currentEquation);
        this.equationHistory.push(`${this.currentEquation}=${this.result}`);
        this.currentEquation = this.result;
      } else if (button === 'AC') {
        this.result = 0;
        this.currentEquation = '';
      } else {
        this.currentEquation += button;
      }
    },
    showHistory() {
      this.showingHistory = !this.showingHistory;
    },
  },
  created() {
    this.result = 0;
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500&display=swap');
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Roboto', sans-serif;
}
.calculator {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100vh;
}
.title {
  font-size: 40px;
}
.wrapper {
  width: 280px;
  background-color: #495057;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 4px rgba(0, 0, 0, 0.3);
}
.result {
  padding: 30px 20px;
  background-color: #343a40;
  border: 3px solid #343a40;
  color: #fff;
}
.calculation {
  display: flex;
}
.numbers {
  display: grid;
  grid-template-rows: 1fr 1fr 1fr 1fr;
  grid-template-columns: 1fr 1fr 1fr;
}

.number {
  width: 70px;
  height: 70px;
  background-color: #495057;
  color: #fff;
  border: 1px solid #343a40;
  cursor: pointer;
}
.operators {
  display: flex;
  flex-direction: column;
}
.button {
  width: 70px;
  height: 70px;
  background-color: #fcc419;
  color: #fff;
  border: 1px solid #343a40;
  cursor: pointer;
}
.equation {
  height: 60px;
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr;
}
.equation button {
  background-color: #fcc419;
  color: #fff;
  border: 1px solid #343a40;
}
.history h3 {
  padding: 10px;
  color: #fff;
}
.history ul li {
  color: #fff;
}
.history {
  height: 150px;
  overflow-y: auto;
}
/*style to scroll*/
.history::-webkit-scrollbar {
  width: 8px;
}

.history::-webkit-scrollbar-track {
  background-color: #343a40;
}

.history::-webkit-scrollbar-thumb {
  background-color: #888;
  border-radius: 4px;
}

.history::-webkit-scrollbar-thumb:hover {
  background-color: #555;
}
</style>

<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <div class="col-md-4">
      <table class="table table-bordered">

        <tbody>
          <tr class="output">
            <td class="output" colspan="4">
              {{ currentValue || 0 }}
            </td>
          </tr>
          <tr>
            <!-- <th scope="row">1</th> -->
            <td @click="clearField">C</td>
            <td @click="setNegativeOrPositive">+/-</td>
            <td @click="calculatePercentege">%</td>
            <td @click="processOutput('divide')" class="lastColumn"><i class="fas fa-divide"></i></td>
          </tr>
          <tr>
            <td @click="getNumber('7')">7</td>
            <td @click="getNumber('8')">8</td>
            <td @click="getNumber('9')">9</td>
            <td @click="processOutput('multiply')" class="lastColumn">x</td>
          </tr>
          <tr>
            <td @click="getNumber('4')">4</td>
            <td @click="getNumber('5')">5</td>
            <td @click="getNumber('6')">6</td>
            <td @click="processOutput('subtract')" class="lastColumn">-</td>
          </tr>
          <tr>
            <td @click="getNumber('1')">1</td>
            <td @click="getNumber('2')">2</td>
            <td @click="getNumber('3')">3</td>
            <td @click="processOutput('add')" class="lastColumn">+</td>
          </tr>
          <tr>
            <td @click="getNumber('0')" colspan="2">0</td>
            <td @click="getDot()">.</td>
            <td @click="updateOutput(operator)" class="lastColumn">=</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {

  props: {
    msg: String
  },
  data() {
    return {
      currentValue: '',
      previousValue: null,
      operationFired: false,
      operator: ''
      // operation: ''
    }
  },
  methods: {
    clearField() {
      this.currentValue = '';
    },
    setNegativeOrPositive() {
      this.currentValue = this.currentValue[0] === '-' ? this.currentValue.slice(1) : this.currentValue
    },
    calculatePercentege() {
      this.currentValue = parseFloat(this.currentValue) / 100;
    },
    getNumber(number) {
      if (this.operationFired) {
        this.previousValue = this.currentValue;
        this.currentValue = '';
        this.operationFired = false;
      } else if (this.currentValue === 'Divide by 0') {
        this.currentValue = '';
        this.operationFired = false;
      }
      this.currentValue += number


    },
    getDot() {
      if (this.currentValue.indexOf('.') === -1) {
        this.currentValue = this.currentValue + '.'
      }
    },
    // processOutput(operator) {
    //   if (operator === 'add') {
    //     this.operation = (a, b) => {
    //       return parseFloat(a) + parseFloat(b);
    //     }

    //   }
    //   else if (operator === 'subtract') {
    //     this.operation = (a, b) => {
    //       return parseFloat(a) - parseFloat(b)
    //     }
    //   } else if (operator === 'divide') {
    //     this.operation = (a, b) => {
    //       if (b == 0) {
    //         return this.currentValue = 'Divide by 0'
    //       }
    //       return parseFloat(a) / parseFloat(b)
    //     }
    //   } else if (operator === 'multiply') {
    //     this.operation = (a, b) => {
    //       return parseFloat(a) * parseFloat(b)
    //     }
    //   }


    //   this.previousValue = this.currentValue;
    //   this.operationFired = true;
    // },
    processOutput(mathSign) {
      this.operator = mathSign;
      switch (this.operator) {
        case "add":
          this.operationFired = true;
          return parseFloat(this.previousValue) + parseFloat(this.currentValue);
        case "subtract":
        this.operationFired = true;
          return parseFloat(this.previousValue) - parseFloat(this.currentValue)
          
        case "divide":
        this.operationFired = true;
      
            if (this.currentValue == 0) {
              return this.currentValue = 'Divide by 0'
            }
           return parseFloat(this.previousValue) / parseFloat(this.currentValue);
          
        case "multiply":
        this.operationFired = true;
          return parseFloat(this.previousValue) * parseFloat(this.currentValue)
          
      }
    },
    updateOutput(operator) {
      this.currentValue = this.processOutput(operator)
      console.log(this.currentValue);

      this.previousValue = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.output {
  background-color: #333;
  color: #fff;
}

.lastColumn {
  background-color: orange;
  color: #fff;
}

.lastColumn:active {
  background-color: #333;
  color: #fff;
}
</style>

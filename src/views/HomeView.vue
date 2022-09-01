
  <template>
  <div class="container">
    <div class="calc">
      <div class="screen">{{ numOne !== '' ? (sum !== '' ? sum : numOne + operator + numTwo) : 0 }}</div>
      <div class="keypad">
        <div class="buttons">
          <button @click.prevent="addNum('7')">7</button>
          <button @click.prevent="addNum('8')">8</button>
          <button @click.prevent="addNum('9')">9</button>
          <button @click.prevent="del()" class="del">DEL</button>
          <button @click.prevent="addNum('4')">4</button>
          <button @click.prevent="addNum('5')">5</button>
          <button @click.prevent="addNum('6')">6</button>
          <button @click.prevent="addOperator('+')">+</button>
          <button @click.prevent="addNum('1')">1</button>
          <button @click.prevent="addNum('2')">2</button>
          <button @click.prevent="addNum('3')">3</button>
          <button @click.prevent="addOperator('-')">-</button>
          <button @click.prevent="addComma()">.</button>
          <button @click.prevent="addNum('0')">0</button>
          <button @click.prevent="addOperator('/')">/</button>
          <button @click.prevent="addOperator('x')">x</button>
        </div>
        <div class="footer">
          <div @click="reset()" class="reset">C</div>
          <div @click.prevent="equal()" class="equal">=</div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { ref } from 'vue';

export default {
  setup() {
    const numOne = ref('')
    const operator = ref('')
    const numTwo = ref('')
    const sum = ref('')
    const equal = () => {
      if (numOne.value !== '' && numTwo.value !== '' && operator.value !== '') {
        if (operator.value == '+') {
          sum.value = parseFloat(numOne.value) + parseFloat(numTwo.value)
        } else if (operator.value == '-') {
          sum.value = parseFloat(numOne.value) - parseFloat(numTwo.value)
        } else if (operator.value == '/') {
          sum.value = parseFloat(numOne.value) / parseFloat(numTwo.value)
        } else if (operator.value == 'x') {
          sum.value = parseFloat(numOne.value) * parseFloat(numTwo.value)
        }
      }
    }
    const addOperator = (sentOperator) => {
      if (numOne.value !== '') {
        operator.value = sentOperator;
      } else {
        alert('Add first number')
      }
    }
    const addNum = (num) => {
      if (numOne.value == '' && operator.value == '') {
        numOne.value = num
      } else if (numOne.value !== '' && operator.value == '') {
        numOne.value += num
      } else if (numOne.value !== '' && operator.value !== '' && numTwo.value == '') {
        numTwo.value = num
      } else if (numOne.value !== '' && operator.value !== '' && numTwo.value !== '') {
        numTwo.value += num
      }
    }
    const reset = () => {
      numOne.value = ''
      numTwo.value = ''
      operator.value = ''
      sum.value = ''
    }
    const del = () => {
      if (numOne.value !== "" && operator.value == "" && numTwo.value == "") {
        numOne.value = numOne.value.slice(0, -1)
      }
      else if (numOne.value !== "" && operator.value !== "" && numTwo.value == "") {
        operator.value = operator.value.slice(0, -1)
      }
      else if (numOne.value !== "" && operator.value !== "" && numTwo.value !== "") {
        numTwo.value = numTwo.value.slice(0, -1)
      }
    }
    const addComma = () => {
      if (numOne.value !== '' && operator.value == '') {
        numOne.value += '.'
      } else if (numOne.value !== '' && operator.value !== '' && numTwo.value !== '') {
        numTwo.value += "."
      }
    }
    return {
      numOne,
      numTwo,
      operator,
      sum,
      equal,
      addNum,
      addOperator,
      reset,
      del,
      addComma
    }
  }
}
</script>
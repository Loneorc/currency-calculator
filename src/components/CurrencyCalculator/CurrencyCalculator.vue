<script>
import CalculatorNavigation from "@/components/Navigation/Navigation.vue";
import { defineComponent } from "vue";
import History from "@/components/History/History.vue";
export default defineComponent({
  name: "CurrencyCalculator",
  components: {
    History,
    navigation: CalculatorNavigation,
  },
  data() {
    return {
      amount: 0,
      exchangeRate: 0,
      conversion: "toDollar",
      result: 0,
      counter: 0,
      currentCalculation: {
        id: 0,
        amount: 0,
        exchangeRate: 0,
        result: 0,
      },
    };
  },
  methods: {
    calculate() {
      if (this.conversion === "toDollar") {
        this.result = this.resultDollar;
      } else {
        this.result = this.resultEuro;
      }
      this.updateHistory();
    },
    updateHistory() {
      this.currentCalculation = {
        id: this.counter,
        amount: this.amount,
        exchangeRate: this.exchangeRate,
        result: this.result,
      };
      this.counter++;
    },
    convertTo(event) {
      this.conversion = event.target.dataset.conversion;
      this.result = 0;
    },
    resetValues() {
      this.amount = 0;
      this.exchangeRate = 0;
      this.result = 0;
      this.conversion = "toDollar";
    },
    someMethod(myData){
      console.log(`Message from child: ${myData}`)
      this.amount = myData;
    }
  },
  computed: {
    setCurrencySymbol() {
      return this.conversion === "toDollar" ? "fa fa-eur" : "fa fa-usd";
    },
    resultDollar() {
      const result = this.amount * this.exchangeRate;
      const invalid = isNaN(result);
      return invalid ? 0 : result;
    },
    resultEuro() {
      const result = this.amount / this.exchangeRate;
      const invalid = isNaN(result) || !isFinite(result);
      return invalid ? 0 : result;
    },
  },
});
</script>

<template>
  <header class="content columns is-centered">
    <div class="column is-one-quarter">
      <h1>Currency Calculator</h1>
      <navigation class="nav-item" @click="convertTo"></navigation>
    </div>
  </header>
  <main @keyup.esc="resetValues" class="content columns is-centered">
    <div class="column is-one-quarter">
      <template v-if="conversion === 'toDollar'">
        <div class="field">
          <label class="label" for="amount">Amount (Euro): </label>
          <div class="control has-icons-left">
            <input class="input is-primary" @keyup.shift.alt.e="convertTo" data-conversion="toEuro" type="text" id="amount"
                   v-model="amount" />
            <span class="icon is-small is-left"><i :class="setCurrencySymbol"></i></span>
          </div>
        </div>
        <div class="field">
          <label class="label" for="exchangeRate">Exchange rate: </label>
          <div class="control has-icons-left">
            <input class="input is-primary" type="text" id="exchangeRate" v-model="exchangeRate" />
            <span class="icon is-small is-left">
              <i class="fa fa-line-chart"></i>
            </span>
          </div>

        </div>
        <p>Dollar: {{ result }}</p>
      </template>

      <template v-else>
        <div class="field">
          <label class="label" for="amount">Amount (Dollar): </label>
          <div class="control has-icons-left">
            <input class="input is-primary" @keyup.shift.alt.d="convertTo" data-conversion="toDollar" type="text" id="amount"
                   v-model="amount" />
            <span class="icon is-small is-left">
              <i :class="setCurrencySymbol"></i>
            </span>
          </div>
        </div>
        <div class="field">
          <label class="label" for="exchangeRate">Exchange rate: </label>
          <div class="control has-icons-left">
            <input class="input is-primary" type="text" id="exchangeRate" v-model="exchangeRate" />
            <span class="icon is-small is-left"><i class="fa fa-line-chart"></i></span>
          </div>
        </div>
        <p>Euro: {{ result }}</p>
      </template>

      <button class="button is-primary" type="button" @click="calculate">Calculate</button>

      <History v-bind:history="currentCalculation" :conversion="conversion"
               @copy-amount="someMethod">

        <template #heading="{message}">
          <p>{{message}}</p>

        </template >

        <template>
          <thead>
          <tr>
            <th>AMOUNT</th>
            <th>EXCHANGE RATE</th>
            <th>RESULT</th>
            <th></th>
          </tr>
          </thead>

        </template>

      </History>

    </div>
  </main>
</template>

<style scoped>
header {
  margin-top: 25px;
}
</style>
<script>
import { defineComponent } from "vue";
export default defineComponent({
  name: "History",
  props: {
    conversion: {
      type: String,
      required: false,
      default: "toDollar",
      validator: function (value){
        return value === 'toDollar' || value === 'toEuro';
      },

    },
    history: {
      type: Object,
      required: true,
      validator: (value) => typeof value.result === 'number',
    },
  },
  data() {
    return {
      calculationHistory: [],
      message: 'This is the calculation history',
    };
  },
  watch: {
    history() {
      this.updateHistory();
    },
  },
  computed: {
    amountCurrencySymbol() {
      return this.conversion === "toDollar" ? "fa fa-eur" : "fa fa-usd";
    },
    resultCurrencySymbol() {
      return this.conversion === "toDollar" ? "fa fa-usd" : "fa fa-eur";
    },
  },
  methods: {

    copyAmount(value){

      this.$emit("copyAmount", value)
    },

    updateHistory() {
      this.calculationHistory.push(
          {
            ...this.history, // -> you can use this Spread operator or comment out the following 4 lines
            // id: this.history.id,
            // amount: this.history.amount,
            // exchangeRate: this.history.exchangeRate,
            // result: this.history.result,
            amountCurrencySymbol: this.amountCurrencySymbol,
            resultCurrencySymbol: this.resultCurrencySymbol,
          },
      );
    },
  },
});
</script>

<template>
  <table class="table is-striped is-narrow">

    <slot name="heading" :message="message">
    <h3>Something</h3>

    </slot>

    <slot>
      <thead>
      <tr>
        <th >Amount</th>
        <th>Exchange rate</th>
        <th>Result</th>
        <th></th>
      </tr>
      </thead>
    </slot>

    <tbody>
    <tr v-for="item in calculationHistory" :key="item.id">
      <td>{{ item.amount }}&nbsp;<i class="fa" :class="item.amountCurrencySymbol"></i></td>
      <td>{{ item.exchangeRate }}</td>
      <td>{{ item.result }}&nbsp;<i class="fa" :class="item.resultCurrencySymbol"></i></td>
      <td>
        <i class="fa fa-edit is-clickable" rel="tooltip" title="Copy amount back to form " @click="copyAmount(item.amount)">
        </i>
      </td>
    </tr>
    </tbody>

  </table>
</template>

<style scoped>
</style>
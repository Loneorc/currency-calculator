<script>
import {defineComponent} from "vue";
import CurrencyCalculator from './components/CurrencyCalculator/CurrencyCalculator.vue';
import ListExercise from './components/ListExercise/ListExercise.vue';
import Counter from "@/components/Counter/Counter.vue";

export default defineComponent({
  components: {
    'currency-calculator': CurrencyCalculator,
    ListExercise,
    Counter
  }
})


</script>

<template>

  <currency-calculator></currency-calculator>


</template>

<style scoped>

</style>

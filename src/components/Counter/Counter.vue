<script>

import {defineComponent} from "vue";
export default defineComponent( {
  name: 'Counter',
  data() {
    return {
      counter: 0
    }

  },
  methods: {
    inc(){
      this.counter++;
    },
    dec(){
      this.counter--;
    },
  },
  computed: {
    even(){
      return this.counter % 2 === 0;
    }
  }

});
</script>

<template>
  <h1>Counter app</h1>
  <div>
    Current Counter Value:<strong> {{counter}}</strong>
    <div>
      <button @click="inc">Increase</button>
      <button :disabled="even" @click="dec">Decrease</button>
    </div>

  </div>
</template>

<style scoped>

</style>
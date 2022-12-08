<script>


import {defineComponent} from "vue";

export default defineComponent( {
  name: 'ListExercise',
  data(){
    return {
      person: {
        firstname: 'Daniel',
        lastname: 'Kovács',
        age: 32
      }
    }
  }
});

</script>

<template>

  <h1></h1>

  <ul>
    <li v-for="(item, key, index) in person">{{key}} : {{item}} : {{index}}</li>
  </ul>

</template>
<style scoped>

</style>
<script>
import {defineComponent} from "vue";

export default defineComponent({
  name: "Navigation"
});
</script>

<template>

  <nav>
    <ul>
      <li><a href="#" data-conversion="toDollar">Euro -> Dollar</a></li>
      <li><a href="#" data-conversion="toEuro">Dollar -> Euro</a></li>

    </ul>
  </nav>

</template>
<style scoped>
</style>
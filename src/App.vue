

<template>
  <main>
    <Milionare />
  </main>
</template>

<script>
import { RouterView } from 'vue-router';
import Milionare from './components/Milionare.vue';

export default {
  components: {
    Milionare,
    RouterView
  }
}
</script>

<style scoped></style>

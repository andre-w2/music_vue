<template>
  <div class="container-fluid">
    <Home />
  </div>
</template>

<script>
import { defineComponent } from 'vue';
import Home from '@/views/Home.vue';

export default defineComponent({
  name: 'App',
  components: {Home}
})
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
</style>
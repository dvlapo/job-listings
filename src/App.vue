<template>
  <Header />
  <Jobs />
</template>

<script>
import Header from './components/Header.vue';
import Jobs from './components/Jobs.vue';

export default {
  name: 'App',
  components: {
    Header,
    Jobs,
  },
};
</script>

<style>
#app {
  font-family: 'Spartan', sans-serif;
  background-color: hsl(180, 52%, 96%);
  min-height: 100vh;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>

<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
import MainPage from './components/MainPage';

export default {
  name: 'App',
  components: {
    MainPage,
  },
};
</script>

<style></style>

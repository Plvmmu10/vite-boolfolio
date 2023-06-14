
<template>
  <AppHeader />

  <main>
    <router-view></router-view>
  </main>
</template>


<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';

export default {
  name: 'App',
  components: {
    AppHeader
  }
}
</script>


<style lang="scss" scoped></style>

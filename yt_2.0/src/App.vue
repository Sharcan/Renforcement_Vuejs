<template>
  <v-app>

    <TopBar></TopBar>

    <MainYt></MainYt>

  </v-app>
</template>

<script>
import TopBar from './components/TopBar';
import MainYt from './components/MainYt';

export default {
  name: 'App',

  components: {
    TopBar,
    MainYt
  },

  data: () => ({
    //
  }),
};
</script>

<template>
  <v-app>
    <v-main>
      <div class="app">
        <Popup/>
      </div>
    </v-main>
  </v-app>
</template>

<script>
import Popup from './components/Popup';

export default {
  name: 'App',

  components: {
    Popup,
  },

  data: () => ({
    //
  }),
};
</script>

<style>
  .app {
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  } 
</style>

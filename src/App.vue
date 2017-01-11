<template>
  <div id="app">
    <ticket-store></ticket-store>
  </div>
</template>

<script>
import TicketStore from './pages/ticket-store.vue'

export default {
  name: 'app',
  components: {
    TicketStore
  }
}
</script>

<style>
html {
  box-sizing: border-box;
  font-size: 16px;
  line-height: 1.5;
  height: 1px;
  min-height: 100%;

  *, *:before, *:after {
    box-sizing: inherit;
  }
}

*, html, body {
  margin: 0;
  padding: 0;
}

body, #app {
  height: 1px;
  min-height: 100%;
}

#app {
  font-family: 'Lato', 'Helvetica Neue', Helvetica, Arial, sans-serif;
  font-weight: 400;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #fff;
}
</style>

<template>
  <div id='app'>
    <navbar></navbar>
    <typing-area></typing-area>
  </div>
</template>

<script>
import TypingArea from './components/TypingArea'
import Navbar from './components/Navbar'

export default {
  name: 'app',
  components: {
    TypingArea,
    Navbar
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Roboto:300,400,500,700');

* {
  margin: 0;
  padding: 0;
}
#app {
  min-height: 100vh;
}
</style>

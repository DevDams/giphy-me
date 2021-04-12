<template>
  <div>
    <Header />
    <Giphy />
  </div>
</template>

<script>
import Header from './components/Header'
import Giphy from './components/Giphy'

export default {
  name: 'App',
  components: {
    Giphy,
    Header
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Lexend:wght@100;300;400;500;600;700;800&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #ECF0F3;
  font-family: 'Lexend', sans-serif;
}

#app {
  text-align: center;
}
</style>

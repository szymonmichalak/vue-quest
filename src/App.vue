<template>
  <div id="app">
    <Container/>
    <Channel/>
    <Container/>
  </div>
</template>

<script>
import Container from './components/Container'
import Channel from './components/Channel'

export default {
  name: 'App',
  components: {
    Container,
    Channel
  }
}
</script>

<style>
#app {
  display: flex;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto 0 auto;
  width: 600px;
}
</style>

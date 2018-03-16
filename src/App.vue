<template>
  <div id="app">
    <button
      class="button"
      @click="addWaterTo"
    >
      💦
    </button>
    <div class="row">
      <Container
        id="A"
        :container-height="containerHeight"
        :channel-level="channelLevelA"
        :water-level="waterLevelA"
      />
      <Channel
        :margin-bottom="channelLevelB"
      />
      <Container
        id="B"
        :container-height="containerHeight"
        :margin-top="containerDifference"
        :channel-level="channelLevelB"
        :water-level="waterLevelB"
      />
    </div>
  </div>
</template>

<script>
import EventBus from './utils/EventBus'
import Container from './components/Container'
import Channel from './components/Channel'

const WATER_STEP = 20

export default {
  name: 'App',
  components: {
    Container,
    Channel
  },
  data: function () {
    return {
      containerHeight: 200,
      containerDifference: 40,
      channelLevelB: 80,
      waterLevelA: 20,
      waterLevelB: 0
    }
  },
  computed: {
    channelLevelA: function () {
      return this.channelLevelB - this.containerDifference
    }
  },
  methods: {
    addWaterTo: function () {
      EventBus.$emit('addWater', { id: 'A', amount: WATER_STEP })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px auto 0 auto;
  width: 600px;
}

.row {
  display: flex;
}

.button {
  background-color: rgb(133, 235, 232);
  border-radius:25px;
  cursor:pointer;
  color: rgb(56, 70, 93);
  padding:16px 20px;
  text-decoration:none;
  text-shadow:0 1px 0 #283966;
}

.button:hover {
  background-color: rgb(56, 70, 93);
  color: #fff;
}

.button:focus {
  outline: none;
}
</style>

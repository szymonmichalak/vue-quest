<template>
  <div id="app">
    <button @click="addWaterToA">+</button>
    <Container
      :channel-level="channelLevelB"
      :water-level="waterLevelA"
    />
    <Channel
      :margin-bottom="channelLevelB"
    />
    <Container
      :margin-top="containerDifference"
      :channel-level="channelLevelB"
      :water-level="waterLevelB"
    />
  </div>
</template>

<script>
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
    addWaterToA: function () {
      this.waterLevelA += WATER_STEP
      if (this.waterLevelA > this.channelLevelA) {
        let amountOfWaterForB = this.waterLevelA - this.channelLevelA
        amountOfWaterForB = amountOfWaterForB > 0 ? amountOfWaterForB : 0
        setTimeout(() => {
          this.addWaterToB(amountOfWaterForB)
        }, 500)
      }
    },
    addWaterToB: function (amountOfWater) {
      if (this.waterLevelB - this.containerDifference < this.waterLevelA) {
        this.waterLevelA -= WATER_STEP
        this.waterLevelB += WATER_STEP
      }
      if ((this.waterLevelB - this.containerDifference) === this.waterLevelA) {
        this.waterLevelA += (WATER_STEP / 2)
        this.waterLevelB += (WATER_STEP / 2)
      }
      if ((this.waterLevelB - this.containerDifference) > this.waterLevelA) {
        this.waterLevelA -= (WATER_STEP / 2)
        this.waterLevelB += (WATER_STEP / 2)
      }
    }
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

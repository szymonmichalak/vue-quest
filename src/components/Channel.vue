<template>
  <div
    class="channel"
    :style="containerStyle"
  >
    <div
      class="water"
      :style="waterStyle"
    />
  </div>
</template>

<script>
import EventBus from '../utils/EventBus'
const maxHeight = 20

export default {
  name: 'Channel',
  props: {
    marginBottom: {
      type: Number,
      default: 0
    }
  },
  data: function () {
    return {
      level: 0
    }
  },
  computed: {
    containerStyle () {
      return `margin-bottom: ${this.marginBottom}px`
    },
    waterStyle () {
      return `height: ${this.level < maxHeight ? this.level : maxHeight}px`
    }
  },
  created () {
    EventBus.$on('fillChannel', () => {
      this.level = maxHeight
    })

    EventBus.$on('pourChannel', () => {
      this.level = 0
    })
  }
}
</script>

<style scoped>
.channel {
  background: rgb(93, 182, 134);
  height: 10px;
  width: 50px;
  border-bottom: 15px solid rgb(56, 70, 93);
  border-top: 15px solid rgb(56, 70, 93);
  display: flex;
  flex-direction: column-reverse;
  align-self: flex-end;
  margin: 0 -15px;
  z-index: 1;
}

.water {
  width: 100%;
  background-color: rgb(133, 235, 232);
  transition: height 500ms;
  color: white;
  text-align: center;
  font-size: 0.75rem;
  align-self: flex-end;
}
</style>

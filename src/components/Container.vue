<template>
  <div
    class="container"
    :style="containerStyle"
  >
    <div
      class="water"
      :style="waterStyle"
    />
  </div>
</template>

<script>
import { debounce } from 'lodash'
import EventBus from '../utils/EventBus'

export default {
  name: 'Container',
  props: {
    id: {
      type: String,
      required: true
    },
    containerHeight: {
      type: Number,
      default: 0
    },
    marginTop: {
      type: Number,
      default: 0
    },
    channelLevel: {
      type: Number,
      default: 0
    },
    waterLevel: {
      type: Number,
      default: 0
    }
  },
  data: function () {
    return {
      level: this.waterLevel
    }
  },
  computed: {
    waterStyle () {
      let height = this.level
      return `height: ${height}px`
    },
    containerStyle () {
      return `
      height: ${this.containerHeight}px;
      margin-top: ${this.marginTop}px;
      `
    }
  },
  watch: {
    level: function () {
      if (this.level > this.channelLevel) {
        EventBus.$emit('fillChannel')
      } else {
        EventBus.$emit('pourChannel')
      }
    }
  },
  methods: {
    flowWater: debounce((data) => {
      EventBus.$emit('flowWater', data)
    }, 500)
  },
  created () {
    EventBus.$on('addWater', (data) => {
      if (data.id === this.id && this.level < this.containerHeight) {
        this.level += data.amount

        const waterExcess = this.level - this.channelLevel
        if (!data.skipPhysics && waterExcess > 0) {
          this.flowWater({ from: this.id, amount: waterExcess })
        }
      }
    })

    EventBus.$on('pourWater', (data) => {
      if (data.id === this.id) {
        this.level -= data.amount
      }
    })

    EventBus.$on('flowWater', (data) => {
      if (data.from !== this.id) {
        if (this.level < this.containerHeight) {
          if (this.level + data.amount <= this.channelLevel) {
            EventBus.$emit('addWater', { id: this.id, amount: data.amount, skipPhysics: true })
            EventBus.$emit('pourWater', { id: data.from, amount: data.amount })
          } else {
            const waterExcess = this.level - this.channelLevel
            const waterLevelDifference = (data.amount - waterExcess) / 2

            EventBus.$emit('addWater', { id: this.id, amount: waterLevelDifference, skipPhysics: true })
            EventBus.$emit('pourWater', { id: data.from, amount: waterLevelDifference })
          }
        } else {
          EventBus.$emit('addWater', Object.assign({}, data, { skipPhysics: true }))
        }
      }
    })
  }
}
</script>

<style scoped>
.container {
  background: rgb(93, 182, 134);
  height: 200px;
  width: 100px;
  border-left: 15px solid rgb(56, 70, 93);
  border-right: 15px solid rgb(56, 70, 93);
  border-bottom: 15px solid rgb(56, 70, 93);
  display: flex;
  flex-direction: column-reverse;
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

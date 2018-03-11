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
export default {
  name: 'Container',
  props: {
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
  computed: {
    waterStyle () {
      let height = this.waterLevel
      return `height: ${height}px`
    },
    containerStyle () {
      return `
      height: ${this.containerHeight}px;
      margin-top: ${this.marginTop}px;
      `
    }
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

<template>
  <div class="channel">
    <div class="water"/>
  </div>
</template>

<script>
export default {
  name: 'Channel'
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
  height: 100px;
  background-color: rgb(133, 235, 232);
  transition: height 500ms;
  color: white;
  text-align: center;
  font-size: 0.75rem;
  align-self: flex-end;
}
</style>

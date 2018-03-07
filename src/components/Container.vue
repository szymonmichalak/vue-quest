<template>
  <div class="container">
    <div class="water"/>
  </div>
</template>

<script>
export default {
  name: 'Container'
}
</script>

<style scoped>
.container {
  background: rgb(93, 182, 134);
  height: 150px;
  width: 100px;
  border-left: 15px solid rgb(56, 70, 93);
  border-right: 15px solid rgb(56, 70, 93);
  border-bottom: 15px solid rgb(56, 70, 93);
  display: flex;
  flex-direction: column-reverse;
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

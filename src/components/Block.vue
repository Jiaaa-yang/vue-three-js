<template>
  <div :class="{ initial: isInitial, waiting: isWaiting, active: isActive}"></div>
  <p>Reaction time is: {{ reactionTime }} ms</p>
</template>

<script>
export default {
  props: ['isInitial', 'isWaiting', 'isActive', 'reactionTime'],
}
</script>

<style scoped>
div {
  width: 500px;
  height: 500px;
  margin: auto;
}

.initial {
  background-color: beige;
}

.waiting {
  background-color: darkred;
}

.active {
  background-color: chartreuse;
}
</style>
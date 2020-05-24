<template>
  <div @click="$emit('play', note)">
    <span>{{ note }}</span>
  </div>
</template>

<script>
export default {
  name: 'TonePanel',
  props: {
    note: {
      type: String,
      required: true
    }
  }
}
</script>

<style scoped>
div {
  width: 100%;
  height: 100%;

  color: #fff;
  font-weight: bold;

  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: sans-serif;

  -webkit-touch-callout: none;

  -webkit-user-select: none; /* Safari */
  -khtml-user-select: none;
  -moz-user-select: none; /* Firefox */
  -ms-user-select: none; /* IE10+/Edge */
  user-select: none; /* Standard */

  -webkit-tap-highlight-color: transparent;
}
</style>

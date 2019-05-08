<template>
  <div class="space" v-on:click="$emit('space-selected', spaceIndex)">{{ mark }}</div>
</template>

<script>
export default {
  name: "Space",
  props: ['spaceIndex', 'mark']
};
</script>

<style scoped>
.space {
  align-items: center;
  background: white;
  display: flex;
  font-size: 2rem;
  justify-content: center;
}

.space:hover {
  background: lightgray;
}
</style>

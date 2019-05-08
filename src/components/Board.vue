<template>
  <div class="board">
    <space v-for="(mark, index) in spaces" v-bind:key="index" v-bind:spaceIndex="index" v-bind:mark="mark" v-on:space-selected="spaceSelected"></space>
  </div>
</template>

<script>
import Space from "./Space.vue";

export default {
  name: "Board",
  components: {
    Space
  },
  props: ['spaces', 'disabled'],
  methods: {
    spaceSelected(spaceIndex) {
      if (!this.disabled) {
        this.$emit('space-selected', spaceIndex);
      }
    },
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.board {
  background: black;
  /* TODO: I'm pretty sure there's a better way to do this Grid layout... */
  display: grid;
  grid-gap: 5px;
  grid-template-columns: repeat(3, 75px);
  grid-template-rows: repeat(3, 75px);
  margin: 0 auto;
  width: calc(75px * 3 + 5px * 2);
}
</style>

<template>
  <div class="row-container">
    <cell
      v-for="(cell, index) in row"
      :value="cell"
      :rowIndex="rowIndex"
      :cellIndex="index"
      :clickMethod="clickMethod"
      :key="index"
    />
  </div>
</template>

<script>
import Cell from './Cell';

export default {
  name: 'Row',
  components: {
    Cell,
  },
  props: {
    row: {
      type: Array,
      default: () => [],
    },
    rowIndex: {
      type: Number,
      default: 0,
    },
    clickMethod: {
      type: Function,
      default: () => 'clickMethod fucked',
    },
  },
  data() {
    return {
      msg: 'Welcome to Your Row',
    };
  },
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.row-container {
  display: flex;
  align-content: center;
  justify-content: center;
  /* border: 4px solid #000000; */
}
</style>

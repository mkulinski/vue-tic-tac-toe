<template>
  <div class="cell-container" @click="onClicky">
    {{ value }}
  </div>
</template>

<script>
export default {
  name: 'Cell',
  props: {
    value: {
      type: String,
      default: '',
    },
    rowIndex: {
      type: Number,
      default: 0,
    },
    cellIndex: {
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
    };
  },
  methods: {
    onClicky() {
      this.clickMethod(this.rowIndex, this.cellIndex);
    },
  },
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cell-container {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 192px;
  width: 180px;
  border: 4px solid #000000;
  font-size: 56px;
  font-weight: 800;
}
</style>

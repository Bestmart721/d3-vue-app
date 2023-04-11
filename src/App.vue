<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div ref="svg"></div>
  </div>
</template>

<script>
import * as d3 from 'd3';

export default {
  name: 'HelloWorld',
  data() {
    return {
      msg: 'D3.js and Vue!',
    };
  },
  mounted() {
    const svg = d3.select(this.$refs.svg)
      .append('svg')
      .attr('width', 500)
      .attr('height', 500);

    svg.append('circle')
      .attr('cx', 250)
      .attr('cy', 250)
      .attr('r', 50)
      .attr('fill', 'blue');
  },
};
</script>

<style scoped>
h1 {
  font-size: 2em;
  font-weight: bold;
  margin-bottom: 0.5em;
}
</style>

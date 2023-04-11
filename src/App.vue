<template>
  <div class="hello">
    <div ref="svg"></div>
  </div>
</template>

<script>
import * as d3 from 'd3';
import { rates } from './data.js'

export default {
  name: 'HelloWorld',
  data() {
    return {
      rates: rates
    };
  },
  mounted() {
    const svg = d3.select(this.$refs.svg)
      .append('svg')
      .attr('width', 1000)
      .attr('height', 1000)
      .append('g')
      .attr('transform', `translate(350,250)`);

    const x = d3.scaleLinear()
      .domain(d3.extent(this.rates, d => d.year))
      .range([0, 400]);

    const y = d3.scaleLinear()
      .domain([0, d3.max(this.rates, d => d.rate)])
      .range([230, 0]);

    const line = d3.line()
      .x(d => x(d.year))
      .y(d => y(d.rate));

    svg.append('path')
      .datum(this.rates)
      .attr('fill', 'none')
      .attr('stroke', 'red')
      .attr('stroke-width', 3)
      .attr('d', line);

    const xAxis = d3.axisBottom(x)
      .tickFormat(d3.format('d'));
    const yAxis = d3.axisLeft(y);

    svg.append('g')
      .attr('transform', `translate(0,230)`)
      .call(xAxis)
      .append('text')
      .attr('x', 215)
      .attr('y', 40)
      .attr('fill', 'black')
      .text('year');
      
    svg.append('g')
      .call(yAxis)
      .append('text')
      .attr('x', -150)
      .attr('y', -40)
      .attr('fill', 'black')
      .attr('transform', `rotate(-90)`)
      .attr('text-anchor', 'middle')
      .text('rate');
      
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
<template>
    <div class="particle-system">
      <svg ref="svg" width="800" height="600"></svg>
    </div>
  </template>
  
  <script>
  import * as d3 from 'd3';
  import { forceSimulation, forceX, forceY, forceCollide } from 'd3-force';
  
  export default {
    name: 'ParticleSystem',
    mounted() {
      const svg = d3.select(this.$refs.svg);
  
      // Define the particles
      const particles = d3.range(200).map(() => ({
        x: Math.random() * 800,
        y: Math.random() * 600,
        vx: Math.random() * 2 - 1,
        vy: Math.random() * 2 - 1
      }));
  
      // Define the forces
      const simulation = forceSimulation(particles)
        .force('x', forceX().strength(0.05))
        .force('y', forceY().strength(0.05))
        .force('collide', forceCollide().radius(5));
  
      // Define the particle elements
      const particle = svg.selectAll('.particle')
        .data(particles)
        .enter().append('circle')
        .attr('class', 'particle')
        .attr('r', 5)
        .attr('cx', d => d.x)
        .attr('cy', d => d.y)
        .style('fill', 'white');
  
      // Define the animation
      simulation.on('tick', () => {
        particle.attr('cx', d => d.x)
          .attr('cy', d => d.y);
      });
    },
  };
  </script>
  
  <style scoped>
  .particle-system {
    background-color: black;
  }
  </style>
  
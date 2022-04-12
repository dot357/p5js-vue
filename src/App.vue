<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
  <section>Sound app</section>
  {{pg}}
  <input type="range" v-model="pg">
</template>

<script>
import * as P5 from "p5";
export default {
  data() {
    return {
      pg: 15,
    };
  },
  created() {
    this.cst()
  },
  beforeUnmount(){
    this.$nextTick(() => {
      document.querySelector('canvas').remove()  
    })
  },
  methods: {
    cst(){
      // this is for inside fncs 
      let _insider = this
      const script = function (p5) {
      var speed = 2;
      var posX = 0;
      console.log(window.innerHeight,window.innerWidth-100)
      // NOTE: Set up is here
      p5.setup = (_) => {
        p5.createCanvas(window.innerWidth-100, window.innerHeight-50);
       
      };
      // NOTE: Draw is here
      p5.draw = (_) => {
        // changes color rgb background(0,23,123,0.5) => Intresting
        // p5.background(0); 
        const degree = p5.frameCount *  _insider.pg /3;
        const y = p5.sin(p5.radians(degree)) * _insider.pg;

        p5.push();
        p5.translate(0, p5.height / 2);
        p5.ellipse(posX, y, 50, 50);
        p5.pop();
        posX += speed;

        if (posX > p5.width || posX < 0) {
          speed *= -1;
        }
      };
    };

    new P5(script);
    }
  },
};
</script>

<style>

</style>

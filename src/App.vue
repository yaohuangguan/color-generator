<template>
  <div id="gradient">
    <h1 style="color:aliceblue">Color Generator</h1>
    <input type="color" @input="setGradient()" name="color1" value="#00ff00" class="color1" />
    <input type="color" @input="setGradient()" name="color2" value="#ff00ff" class="color2" />
    <br />
    <button @click="changeToLeft()">Change to left</button>
    <button @click="changeToRight()">Change to right</button>
    <button @click="changeToBottom()">Change to bottom</button>
    <button @click="changeToTop()">Change to top</button>

    <h5 style="color:aliceblue">Current CSS color background</h5>
    <p id="background"></p>
    <p id="left">first input hexcode:</p>
    <p id="right">second input hexcode:</p>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      direction: "right",
      degree: "",
      flag: false
    };
  },
  methods: {
    changeDegree() {
      this.direction = parseFloat(this.degree);
    },
    changeToLeft() {
      this.direction = "left";
    },
    changeToRight() {
      this.direction = "right";
    },
    changeToBottom() {
      this.direction = "bottom";
    },
    changeToTop() {
      this.direction = "top";
    },
    setGradient() {
      const background = document.querySelector("#background");
      const color_1 = document.querySelector(".color1");
      const color_2 = document.querySelector(".color2");
      const right = document.getElementById("right");
      const left = document.getElementById("left");
      if (this.flag) {
        document.body.style.background = `repeating-linear-gradient(${this.direction} deg, ${color_1.value}, ${color_2.value})`;
      } else {
        document.body.style.background = `repeating-linear-gradient(to ${this.direction},${color_1.value},${color_2.value})`;
      }

      right.innerHTML = "first input hexcode: " + color_2.value;
      left.innerHTML = "second input hexcode: " + color_1.value;
      background.textContent = document.body.style.background;
    }
  }
};
</script>

<style>
body {
  font: "Raleway", sans-serif;
  color: rgba(0, 0, 0, 0.5);
  text-align: center;
  text-transform: uppercase;
  letter-spacing: 0.5em;
  top: 15%;
  background: linear-gradient(to right, green, yellow);
}

h1 {
  font: 600 3.5em "Raleway", sans-serif;
  color: rgba(0, 0, 0, 0.5);
  text-align: center;
  text-transform: uppercase;
  letter-spacing: 0.5em;
  width: 100%;
}

p {
  font: 900 1em "Raleway", sans-serif;
  color: rgba(0, 0, 0, 0.5);
  text-align: center;
  text-transform: none;
  letter-spacing: 0.015em;
}
</style>

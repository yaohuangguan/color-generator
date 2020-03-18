<template>
  <div id="gradient">
    <h1 style="color:aliceblue">Color Generator</h1>
    <input type="color" @input="setGradient" name="color1" value="#72c7f5" class="color1" />
    <input type="color" @input="setGradient" name="color2" value="#8000ff" class="color2" />
    <br />
    <button class="direction-button" @click="changeToLeft">Change to left</button>
    <button class="direction-button" @click="changeToRight">Change to right</button>
    <button class="direction-button" @click="changeToBottom">Change to bottom</button>
    <button class="direction-button" @click="changeToTop">Change to top</button>

    <h5 style="color:aliceblue">Current CSS color background</h5>
    <span style="display:none;color:#ffffff" class="copy">CSS Copied!</span>
    <p id="background" class="copy-text" @click="handleCopy"></p>
    <p id="left" class="copy-text" @click="handleCopy">Input Hexcode:</p>
    <p id="right" class="copy-text" @click="handleCopy">Input Hexcode:</p>

    <div class="claim">Proudly made by Sam Yao</div>
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
    handleCopy(e) {
      let dummy = document.createElement("input");
      let copy = document.querySelector(".copy");
      let content = e.target.textContent.match(/#/g)
        ? e.target.textContent.split(":")[1]
        : e.target.textContent;
      document.body.appendChild(dummy);
      dummy.value = content;
      dummy.select();
      dummy.setSelectionRange(0, 99999);
      document.execCommand("copy");
      document.body.removeChild(dummy);
      copy.style.display = "block";
      setTimeout(() => {
        copy.style.display = "none";
      }, 2000);
    },
    changeDegree() {
      this.direction = parseFloat(this.degree);
    },
    changeToLeft() {
      this.direction = "left";
      this.setGradient();
    },
    changeToRight() {
      this.direction = "right";
      this.setGradient();
    },
    changeToBottom() {
      this.direction = "bottom";
      this.setGradient();
    },
    changeToTop() {
      this.direction = "top";
      this.setGradient();
    },
    setGradient() {
      const background = document.querySelector("#background");
      const color_1 = document.querySelector(".color1");
      const color_2 = document.querySelector(".color2");
      const right = document.getElementById("right");
      const left = document.getElementById("left");
      if (this.flag) {
        document.body.style.background = `linear-gradient(${this.direction} deg, ${color_1.value}, ${color_2.value})`;
      } else {
        document.body.style.background = `linear-gradient(to ${this.direction},${color_1.value},${color_2.value})`;
      }

      right.innerHTML = "Right Input Hexcode: " + color_2.value;
      left.innerHTML = "Left Input Hexcode: " + color_1.value;
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
  background: linear-gradient(to right, #72c7f5, #8000ff);
  background-repeat: no-repeat;
  margin: 0;
  min-height: 100vh;
}
.direction-button{
  color:#fff;
  background-color: #333;
  border-radius: 50px;
  border: none;
  padding: 4px 5px;
  margin: 0 10px;
  outline: none;
}
.color1 {
  width: 80px;
  height: 30px;
}
.color2 {
  width: 80px;
  height: 30px;
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
.claim {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translate(-50%);
}
.copy-text {
  color: aliceblue;
  cursor: pointer;
}
</style>

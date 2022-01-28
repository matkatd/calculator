<template>
  <header>
    <h1>{{ title }}</h1>
    <h2>THEME</h2>
    <div class="theme-picker">
      <li @click="onClick(1)">1</li>
      <li @click="onClick(2)">2</li>
      <li @click="onClick(3)">3</li>

      <div id="slider">
        <div id="dot"></div>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
  props: {
    title: String,
    currentTheme: String,
  },
  data() {
    return {
      newStyle: `{
        grid-column: 2/3;
        justify-self: start; 
        margin-right: 0; 
        margin-left: 3.5px;
      }`,
    };
  },
  methods: {
    onClick(number) {
      if (number === 1) {
        this.newStyle =
          "grid-column: 1/2; justify-self: start; margin-right: 0; margin-left: 3.5px;";
        document.getElementById("dot").style = this.newStyle;
        document.querySelector(":root").style.cssText = `
          --background: hsl(222, 26%, 31%);
          --reset: hsl(225, 21%, 49%);
          --reset-shadow: hsl(224, 28%, 35%);
          --key-color: hsl(30, 25%, 89%);
          --key-shadow: hsl(28, 16%, 65%);
          --equals-button: hsl(6, 63%, 50%);
          --equals-button-shadow: hsl(6, 70%, 34%);
          --answer-box: hsl(224, 36%, 15%);
          --slider-background: hsl(223, 31%, 20%);
          --keypad-background: hsl(223, 31%, 20%);
          --text-color: hsl(221, 14%, 31%);
          --equals-text-color: white;
          --header-text-color: white;
        `;
      } else if (number === 2) {
        this.newStyle = "grid-column: 2/3; justify-self: center; margin: 0;";
        document.getElementById("dot").style = this.newStyle;
        document.querySelector(":root").style.cssText = `
        --background: hsl(0, 0%, 90%);
        --keypad-background: hsl(0, 5%, 81%);
        --slider-background: hsl(0, 5%, 81%);
        --answer-box: hsl(0, 0%, 93%);
        --reset: hsl(185, 42%, 37%);
        --reset-shadow: hsl(185, 58%, 25%);
        --equals-button: hsl(25, 98%, 40%);
        --equals-button-shadow: hsl(25, 99%, 27%);
        --key-color: hsl(45, 7%, 89%);
        --key-shadow: hsl(35, 11%, 61%);
        --text-color: hsl(60, 10%, 19%);
        --equals-text-color: white;
        --header-text-color: black;
        `;
      } else if (number === 3) {
        this.newStyle =
          "grid-column: 3/4; justify-self: end; margin-right: 3.5px; margin-left: 0;";
        document.getElementById("dot").style = this.newStyle;
        document.querySelector(":root").style.cssText = `
        --background: hsl(268, 75%, 9%);
        --keypad-background: hsl(268, 71%, 12%);
        --slider-background: hsl(268, 71%, 12%);
        --answer-box: hsl(268, 71%, 12%);
        --reset: hsl(281, 89%, 26%);
        --reset-shadow: hsl(285, 91%, 52%);
        --equals-button: hsl(176, 100%, 44%);
        --equals-button-shadow: hsl(177, 92%, 70%);
        --key-color: hsl(268, 47%, 21%);
        --key-shadow: hsl(290, 70%, 36%);
        --text-color: hsl(52, 100%, 62%);
        --equals-text-color: hsl(198, 20%, 13%);
        --header-text-color: hsl(52, 100%, 62%);
        `;
      }
    },
  },
};
</script>

<style scoped>
header {
  margin-left: 5%;
  margin-right: 5%;
  display: grid;
  grid-template-columns: 50% 25% 25%;
  align-items: center;
  color: var(--header-text-color);
  margin-bottom: 1vh;
  /* font-size: 1rem; */
}

header > .theme-picker {
  display: grid;
  justify-self: end;
  width: 10vw;
  max-width: 100px;
  min-width: 70px;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  font-size: 0.75rem;
}

.theme-picker li {
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

#slider {
  width: 90%;
  max-width: 90px;
  margin-left: auto;
  margin-right: auto;
  grid-column: 1/4;
  height: 4vw;
  max-height: 30px;
  border-radius: 50px;
  background-color: var(--slider-background);
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  align-items: center;
}

#dot {
  width: 2vw;
  height: 2vw;
  max-width: 20px;
  max-height: 20px;
  margin-left: 3.5px;
  grid-column: 1/2;
  background-color: var(--equals-button);
  border-radius: 50px;
  transition: color 0.3s ease;
}
header > h1 {
  font-size: 3rem;
}
header > h2 {
  font-size: 1rem;
  justify-self: end;
}

@media screen and (max-width: 650px) {
  header {
    font-size: 2rem;
    margin-top: 7%;
  }
  header > h1 {
    margin-bottom: 7%;
    font-size: 2rem;
  }
  header > .theme-picker {
    width: 20vw;
  }
  .slider {
    height: 10vw;
  }
}
</style>

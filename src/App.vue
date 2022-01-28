<template>
  <div id="calculator">
    <Header title="calc" currentTheme="1" />
    <AnswerBlock :output="answer" />
    <Keypad @calculate="makeCalculation" />
  </div>
</template>

<script>
import Header from "./components/Header";
import AnswerBlock from "./components/AnswerBlock";
import Keypad from "./components/Keypad";

export default {
  name: "App",
  components: {
    Header,
    AnswerBlock,
    Keypad,
  },
  data() {
    return {
      answer: "",
    };
  },
  methods: {
    makeCalculation(value) {
      console.log(this.answer);
      const size = this.answer.length;
      const lastChar = this.answer.slice(size - 1, size);
      if (value === "=") {
        if (!isNaN(lastChar)) {
          console.log("did it work?");
          let equals = "";
          try {
            equals = eval(this.answer);
          } catch {
            this.answer = "ERROR";
          }
          if (this.answer.includes(".")) {
            this.answer = equals.toFixed(4);
          } else {
            this.answer = equals.toFixed(0);
          }
        } else return;

        this.$emit("update:answer");
      } else if (value === "DEL") {
        if (this.answer === "undefined" || this.answer === "ERROR") {
          this.answer = "";
        }
        this.answer = this.answer.slice(0, -1);
      } else if (value === "RESET") {
        this.answer = "";
      } else {
        if (this.answer === "undefined" || this.answer === "ERROR") {
          this.answer = "";
        }
        if (value === "x") {
          value = "*";
        }
        if (value === "." && (isNaN(lastChar) || this.answer === "")) {
          value = "0" + value;
        }
        this.answer += value;
        this.$emit("update:answer", this.answer);
      }
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Spartan:wght@700&display=swap");

:root {
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
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html,
body {
  font-family: Arial, Helvetica, sans-serif;
  background: var(--background);
}

#app {
  font-family: "Spartan", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#calculator {
  margin-left: auto;
  border-radius: 5px;
  margin-right: auto;
  width: 60%;
  height: 100%;
  max-height: 550px;
  max-width: 500px;
  margin-top: 1%;
  margin-bottom: 1%;
  background: var(--background);
}

@media screen and (max-width: 650px) {
  #calculator {
    width: 100%;
    height: 100%;
  }
}

li {
  list-style: none;
}
</style>

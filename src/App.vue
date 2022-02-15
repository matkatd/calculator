<template>
  <div id="calculator">
    <Header title="calc" currentTheme="1" />
    <AnswerBlock :output="answer" />
    <Keypad @calculate="makeCalculation" />
  </div>
</template>

<script>
import { evaluate } from "mathjs";
import Header from "./components/Header";
import AnswerBlock from "./components/AnswerBlock";
import Keypad from "./components/Keypad";
// FIXME!!!! It's doing integer division (rounding) do something about it please :)
export default {
  name: "App",
  components: {
    Header,
    AnswerBlock,
    Keypad,
  },
  data() {
    return {
      input: "0",
      storage: "0",
      answer: "0",
      mathStuff: 0.0,
    };
  },
  methods: {
    makeCalculation(value) {
      console.log(this.answer);
      const size = this.storage.length;
      const lastChar = this.storage.slice(size - 1, size);

      if (value === "=") {
        if (!isNAN(lastChar)) {
          let equals = "";
          try {
            equals = evaluate(this.storage);
          } catch {
            this.answer = "ERROR";
          }
          this.answer = equals;
          return;
        }
      } else if (value === "DEL") {
        if (
          this.answer === "undefined" ||
          this.answer === "ERROR" ||
          this.input === "undefined" ||
          this.input === "ERROR"
        ) {
          this.answer = "0";
          this.input = "0";
        } else if (this.answer === "0" || this.input === "0") {
          return;
        } else {
          this.input = this.input.slice(0, -1);
        }
      } else if (value === "RESET") {
        this.input = "0";
        this.storage = "0";
        this.answer = this.input;
      } else {
        if (value === "x") {
          this.input *= 1.0; // Not sure if this will work since this.input is a string, but worth a shot
          this.storage += this.input;
          this.storage += "*";
          this.input = 0;
        } else if (value === "/") {
          this.input *= 1.0;
          this.storage += this.input;
          this.storage += "/";
        } else if (value === "+") {
          this.storage += this.input;
          this.storage += "+";
        } else if (value === "-") {
          this.storage += this.input;
          this.storage += "-";
        } else {
          // value is a number

          if (this.input === "0") {
            this.input = value;
          } else {
            this.input += value;
          }

          this.answer = this.input;
        }
      }
    },

    // if (value === "=") {
    //   if (!isNaN(lastChar)) {
    //     let equals = "";
    //     try {
    //       equals = evaluate(this.answer);
    //     } catch {
    //       this.answer = "ERROR";
    //     }
    //     if (this.answer.includes(".")) {
    //       this.answer = equals.toFixed(4);
    //     } else {
    //       this.answer = equals.toFixed(0);
    //     }
    //   } else return;

    // } else if (value === "DEL") {
    //   if (this.answer === "undefined" || this.answer === "ERROR") {
    //     this.answer = "";
    //   }
    //   this.answer = this.answer.slice(0, -1);
    // } else if (value === "RESET") {
    //   this.answer = "";
    // } else {
    //   if (this.answer === "undefined" || this.answer === "ERROR") {
    //     this.answer = "";
    //   }
    //   if (value === "x") {
    //     value = "*";
    //   }
    //   if (value === "." && (isNaN(lastChar) || this.answer === "")) {
    //     value = "0" + value;
    //   }
    //   this.answer += value;
    //   this.$emit("update:answer", this.answer);
    // }
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
  max-height: 600px;
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

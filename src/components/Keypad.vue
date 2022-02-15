<template>
  <div id="button-grid">
    <Key value="7" class="key" @key-click="sendData" />
    <Key value="8" class="key" @key-click="sendData" />
    <Key value="9" class="key" @key-click="sendData" />
    <Key value="DEL" id="delete" class="key" @key-click="sendData" />
    <Key value="4" class="key" @key-click="sendData" />
    <Key value="5" class="key" @key-click="sendData" />
    <Key value="6" class="key" @key-click="sendData" />
    <Key value="+" class="key" @key-click="sendData" />
    <Key value="1" class="key" @key-click="sendData" />
    <Key value="2" class="key" @key-click="sendData" />
    <Key value="3" class="key" @key-click="sendData" />
    <Key value="-" class="key" @key-click="sendData" />
    <Key value="." class="key" @key-click="sendData" />
    <Key value="0" class="key" @key-click="sendData" />
    <Key value="/" class="key" @key-click="sendData" />
    <Key value="x" class="key" @key-click="sendData" />
    <Key value="RESET" id="reset" class="key" @key-click="sendData" />
    <Key value="=" id="equals" class="key" @key-click="sendData" />
  </div>
</template>

<script>
import Key from "./Key";
export default {
  name: "Keypad",
  components: {
    Key,
  },
  methods: {
    sendData(value) {
      console.log(value);

      this.$emit("calculate", value);
    },
  },
  emits: ["calculate", "key-click"],
};
</script>

<style scoped>
#button-grid {
  background-color: var(--keypad-background);
  margin: 5%;
  border-radius: 10px;
  margin-right: auto;
  margin-left: auto;
  display: grid;
  width: 90%;
  height: 100%;
  max-height: fit-content;
  grid-auto-columns: 1fr;
  grid-auto-rows: 1fr;

  gap: 20px;
  /* place-items: center; */
  padding: 5%;
}

#button-grid .key {
  border: none;
  background-color: var(--key-color);
  color: var(--text-color);
  font-size: 2.25rem;
  font-weight: 600;
  width: 100%;
  height: 100%;
  max-height: 80px;
  max-width: 80px;
  padding-top: 2.5vw;
  padding-bottom: 2.5vw;
  align-self: center;
  justify-self: center;
  text-align: center;
  border-radius: 10px;
  box-shadow: 0px 3px 0px var(--key-shadow), 0px 3px 6px rgba(0, 0, 0, 0.9);
  transition: all 0.1s ease;
  cursor: pointer;
}

.key:active {
  box-shadow: 0px 4px 0px var(--key-shadow), 0px 6px 25px rgba(0, 0, 0, 0.7);
  position: relative;
  top: 2px;
}

#button-grid #delete {
  background-color: var(--reset);
  box-shadow: 0px 3px 0px var(--reset-shadow), 0px 3px 6px rgba(0, 0, 0, 0.9);
  color: white;
}

#button-grid #reset {
  width: 100%;
  background-color: var(--reset);
  box-shadow: 0px 3px 0px var(--reset-shadow), 0px 3px 6px rgba(0, 0, 0, 0.9);
  color: white;
  grid-column: 1/3;
  max-width: 200px;
}

#button-grid #equals {
  width: 100%;
  background-color: var(--equals-button);
  box-shadow: 0px 3px 0px var(--equals-button-shadow),
    0px 3px 6px rgba(0, 0, 0, 0.9);
  color: var(--equals-text-color);
  grid-column: 3/5;
  max-width: 200px;
}

@media screen and (max-width: 650px) {
  .key {
    max-height: 60px;
    max-width: 60px;
  }
}
</style>

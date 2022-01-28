<template>
  <button @click="onPress()">{{ value }}</button>
</template>

<script>
export default {
  name: "Key",
  props: {
    value: String,
  },
  methods: {
    onPress() {
      this.$emit("key-click", this.value);
      console.log(`"you clicked ${this.value}`);
    },
  },
};
</script>

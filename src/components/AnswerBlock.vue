<template>
  <div>{{ output }}</div>
</template>

<script>
export default {
  name: "AnswerBlock",
  props: {
    input: String,
    output: String,
  },
};
</script>

<style scoped>
div {
  margin-right: auto;
  margin-left: auto;

  width: 90%;
  height: 12vh;
  border-radius: 10px;
  background-color: var(--answer-box);
  font-size: 5vh;
  font-weight: 500;
  color: var(--header-text-color);
  display: flex;
  align-items: center;
  padding-right: 10px;
  justify-content: flex-end;
}
</style>

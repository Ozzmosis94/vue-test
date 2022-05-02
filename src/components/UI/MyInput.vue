<template>
  <input :value="modelValue" @input="onInput" class="input" type="text" />
</template>

<script>
export default {
  name: "my-input",
  props: {
    modelValue: String,
  },
  methods: {
    onInput(e) {
      this.$emit("update:modelValue", e.target.value);
    },
  },
};
</script>

<style>
.input {
  width: 100%;
  border: 2px solid grey;
  padding: 10px 15px;
  margin-top: 15px;
}
</style>

<template>
  <button class="btn">
    <slot > </slot>
  </button>
</template>

<script>
export default {
    name:"my-button"
};
</script>

<style>
.btn {

  padding: 10px 15px;
  background: none;
  color: black;
  border: 2px solid grey;
  border: 1px solid grey;
}
button {
  padding: 0;
  border: none;
  font: inherit;
  color: inherit;
  background-color: transparent;
  
}

</style>

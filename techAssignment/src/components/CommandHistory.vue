<script>
export default {
  name: "CommandHistory",
  props: {
    commandValue: {
      type: Object,
      default() {
        return {};
      },
    },
  },
};
</script>

<template>
  <div class="space">
    <div>{{ commandValue.commandHistory }}</div>
    <div>{{ commandValue.message }}</div>
  </div>
</template>

<style>
.space {
  padding: 10px;
}
</style>

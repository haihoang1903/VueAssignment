<script>
export default {
  name: "InputCommand",
  props: {
    propCommandInput: {
      type: String,
      default: "",
    },
    propSetCommandInput: {
      type: Function,
      default(saveInput) {
        return saveInput;
      },
    },
    renderCommand: {
      type: Function,
      default() {
        return {};
      },
    },
  },
  data() {
    return {
      valueCommandInput: this.propCommandInput,
    };
  },
  watch: {
    valueCommandInput(saveInput) {
      this.propSetCommandInput(saveInput);
    },
  },
  methods: {
    renderInput(e) {
      e.preventDefault();
      this.renderCommand();
      this.value = "";
    },
  },
};
</script>

<template>
  <form style="display: flex" v-on:submit="renderInput">
    <input class="input" type="text" v-model="valueCommandInput" />
    <button class="button" type="submit">Enter</button>
  </form>
</template>

<style>
.button {
  background-color: white;
  color: black;
  border: 2px solid #555555;
  border-radius: 5px;
  margin-left: 5px;
}

.button:hover {
  background-color: #555555;
  color: white;
}

.input {
  width: 100%;
  padding: 20px 20px;
  border: 1px solid rgb(0, 0, 0);
  background-color: rgb(0, 0, 0);
  color: white;
}
</style>

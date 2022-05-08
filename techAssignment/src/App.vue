<script>
import InputCommand from "./components/InputCommand.vue";
import CommandHistory from "./components/CommandHistory.vue";

export default {
  name: "App",

  data() {
    return {
      commandInput: "",
      commandInputArray: [],
      arrayValues: [],
      keyValue: {},
    };
  },

  methods: {
    renderInput() {
      var commandInputArray = this.commandInput.split(" ");

      switch (commandInputArray[0]) {
        case "SET":
          // Input must contain 3 words
          if (commandInputArray.length != 3) {
            this.data("ERROR");
          } else {
            // store key and value to array
            this.setKey(commandInputArray[1], commandInputArray[2]);
          }
          break;
        case "GET":
          // Input only function and key to get value
          if (commandInputArray.length != 2) {
            this.loadArrayValues("ERROR");
          } else {
            if (
              // Key must be existed in array
              typeof this.keyValue[commandInputArray[1]] == "string"
            ) {
              this.getKey(commandInputArray[1]);
            } else {
              this.loadArrayValues("ERROR");
            }
          }
          break;
        default:
          this.loadArrayValues("ERROR");
          break;
      }
    },
    setKey(key, itemValue) {
      this.keyValue[key] = itemValue;
      this.loadArrayValues("SUCCESSFULLY");
    },
    getKey(key) {
      let item = this.keyValue[key];
      this.loadArrayValues(item);
    },
    loadArrayValues(text) {
      let values = {};
      values.commandHistory = this.commandInput;
      values.message = text;
      values.count = this.arrayValues.length + 1;
      this.arrayValues.push(values);
    },
    setCommandInput(saveInput) {
      this.commandInput = saveInput;
    },
  },
  components: {
    InputCommand,
    CommandHistory,
  },
};
</script>

<template>
  <div class="page">
    <div>
      <div>
        <div>
          <CommandHistory
            v-for="values in arrayValues"
            :key="values.count"
            v-bind:commandValue="values"
          />
        </div>
      </div>
      <InputCommand
        v-bind:propCommandInput="commandInput"
        v-bind:propSetCommandInput="setCommandInput"
        v-bind:renderCommand="renderInput"
      />
    </div>
  </div>
</template>

<style>
.page {
  border-radius: 5px;
  background-color: #f2f2f2;
  padding: 20px;
  margin: 20px;
  height: 100%;
  border: 2px solid #81818375;
}

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

.input[type="text"] {
  width: 100%;
  padding: 20px 20px;
  border: 1px solid rgb(0, 0, 0);
  border-radius: 4px;
  background-color: rgb(0, 0, 0);
  color: white;
}
</style>

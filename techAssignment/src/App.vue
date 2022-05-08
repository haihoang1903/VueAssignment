<script>
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
    renderInput(e) {
      e.preventDefault();
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
  },
};
</script>

<template>
  <div class="page">
    <div>
      <div>
        <div
          v-for="values in arrayValues"
          :key="values.count"
          style="margin: 17px 0px"
        >
          <div>{{ values.commandHistory }}</div>
          <div>{{ values.message }}</div>
        </div>
      </div>

      <div>
        <form style="display: flex" v-on:submit="renderInput">
          <input class="input" type="text" v-model="commandInput" />
          <button class="button" type="submit">Submit</button>
        </form>
      </div>
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

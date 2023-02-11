<template>
  <div class="Introduction-Line">
    <!-- A simple data message is displayed -->
    <p>My name is {{ msg }} and I am learning Vue.JS 2.0 !!</p>

    <!-- takes and input, stores it in data field and displays it in real time -->
    <input v-model="textfieldMessage" />
    <br />
    <br />
    <span>
      This will display what you enter in the text field :
      <span v-bind:class="redcheckbox ? 'redActive' : 'redNotActive'">{{
        textfieldMessage
      }}</span>
    </span>
    <br />
    <br />

    <!-- two buttons to clear and capitalise the text -->
    <button v-on:click="clearField">Clear</button>
    <button v-on:click="capitalise">Capitalise</button>
    <br />
    <br />

    <!-- used v-model instead of v-if so that the data of 
    checkbox can be changed accordingly -->
    <!-- click the checkbox and text will become red -->
    <input type="checkbox" v-model="redcheckbox" v-on:click="makeitred" />
    <label> Red </label>
    <br />

    <div v-bind:style="{ color: colorSelected.color }">
      {{ textfieldMessage }} Color will change
    </div>
    <select v-model="colorSelected">
      <!-- <option disabled value="">Choose text color</option>
      <option v-bind:value="{ color: Blue }">Blue</option>
      <option v-bind:value="{ color: Green }">Green</option>
      <option v-bind:value="{ color: Purple }">Purple</option>
      <option v-bind:value="{ color: Black }">Black</option>
      <option v-bind:value="{ color: Red }">Red</option> -->
      <option
        v-for="(col, index) in colors"
        v-bind:key="index"
        v-bind:value="{ color: col }"
      >
        {{ col }}
      </option>
      "
    </select>
    <!-- <form>
      <label> Add something: </label>
      <input v-model="newTask" />
      <button>Submit</button>
    </form>
    <ul>
      Tasks:
      <li v-for="{ newTask } in tasks" v-bind:key="index">{{ newTask }}</li>
    </ul> -->
    <div v-if="!isEditing">
      <form @submit.prevent="onSubmit">
        <input v-model="listItems" />
        <button v-on:click="submit">Add to list</button>
      </form>
    </div>

    <div v-else>
      <form @submit.prevent="onSubmit">
        <input v-model="listItems" />
        <button v-on:click="updateTask">Update</button>
      </form>
    </div>

    <!-- <ol>
      <li v-for="item in completeList" :key="item.id">
        {{ item }}
      </li>
    </ol> -->
    <table>
      <tr>
        <th>Task</th>
      </tr>
      <tr v-for="(item, index) in completeList" :key="item.id">
        <td>
          {{ item }}
          <button v-on:click="deleteTask()">Delete</button>
          <button v-on:click="editTask(index, item)">Edit</button>
        </td>
      </tr>
    </table>
  </div>
</template>

<!--  Script -->
<script>
export default {
  name: "Introduction-Line",
  // data: {
  //   redcheckbox: "false",
  // },
  props: { msg: String },
  data: () => {
    // const textfieldMessage = "Shruti";

    return {
      textfieldMessage: "Whatever you write",
      redcheckbox: "false",
      colors: ["Blue", "Green", "Purple", "Black", "Red"],
      colorSelected: {
        color: "Black",
      },
      listItems: "",
      completeList: [],
      selectedIndex: null,
      isEditing: false,
    };
  },

  created: function () {
    console.log("created");
    this.date = new Date();
  },
  mounted: function () {
    console.log("mounted");
    this.date = new Date();
  },
  updated: function () {
    console.log("updated");
  },
  destroyed: function () {
    console.log("destroyed");
    this.message = new Date();
  },

  methods: {
    clearField: function () {
      this.textfieldMessage = "";
    },
    capitalise: function () {
      this.textfieldMessage = this.textfieldMessage.toLocaleUpperCase();
    },
    makeitred: function () {
      this.redcheckbox = !this.redcheckbox;
    },
    submit: function () {
      this.completeList.push(this.listItems);
      this.listItems = "";
    },
    deleteTask: function () {
      this.completeList.pop(this.item);
    },

    editTask: function (index, item) {
      this.item = item;
      this.selectedIndex = index;
      this.isEditing = true;
    },

    updateTask: function () {
      this.completeList.splice(this.selectedIndex, 1, this.item);
      this.isEditing = false;
    },
  },
};
</script>

<!-- Adding CSS which is "scoped" meaning that it is 
limited to this component only -->

<style scoped>
.redNotActive {
  color: rgb(229, 130, 0);
}

.redActive {
  color: rgb(241, 32, 0);
}
p {
  color: rgb(229, 130, 0);
  font-family: "Courier New", Courier, monospace;
}

input {
  margin: 20px 0;
}

table {
  width: 75%;
  box-align: center;
  margin: 0 auto;
}

th,
td {
  border: 1px solid black;
}
</style>

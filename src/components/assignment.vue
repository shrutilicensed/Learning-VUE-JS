<template>
  <div>
    <!-- HEADING -->
    <h2 class="heading">Customer Details</h2>

    <!-- FORM -->
    <form @submit.prevent="onSubmit()">
      <label>First Name</label>
      <input type="text" v-model="firstName" />
      <label>Last Name</label>
      <input type="text" v-model="lastName" />
      <label>Address</label>
      <input type="text" v-model="address" />
      <button v-on:click="addToTable">Add</button>
    </form>

    <!-- TABLE -->
    <table>
      <!-- HEADINGS -->
      <tr>
        <th>First Name</th>
        <th>Last Name</th>
        <th>Address</th>
        <th>Delete and Red</th>
      </tr>

      <!-- DATA|| TR CONNECTS WITH A V-FOR LOOP AND BINDS THE RED CLASSES -->
      <tr
        v-for="(item, index) in rowData"
        :key="index"
        v-bind:class="
          rowData[index].colorCheckbox ? 'redActive' : 'redNotActive'
        "
      >
        <!-- CODE BELOW DOES NOT MAKE A NEW ROW FOR THE DATA -->
        <!-- <td v-for="fName in firstNameList" :key="fName.id">
          {{ fName }}
        </td>
        <td v-for="lname in lastNameList" :key="lname.id">
          {{ lname }}
        </td>
        <td v-for="addressdata in addressList" :key="addressdata.id">
          {{ addressdata }}
        </td> -->
        <td>
          {{ item.firstName }}
        </td>
        <td>
          {{ item.lastName }}
        </td>
        <td>
          {{ item.address }}
        </td>
        <td>
          <button v-on:click="deleteTask(index)">Delete</button>
          <input
            type="checkbox"
            v-model="rowData[index].colorCheckbox"
            :key="index"
            v-on:click="makeitred(index)"
          />
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "CustomerTable",
  data: () => {
    return {
      // firstName: "",
      // firstNameList: [],
      // lastName: "",
      // lastNameList: [],
      // address: "",
      // addressList: [],
      colorCheckbox: false,
      firstName: "",
      lastName: "",
      address: "",
      rowData: [],
    };
  },
  methods: {
    onSubmit: function (event) {
      console.log(event);
    },
    makeitred: function (index) {
      this.rowData[index].colorCheckbox = !this.rowData[index].colorCheckbox;
    },
    // NOTE: DON'T USE POP AS IT WILL POP OUT THE LAST ELEMENT AND NOT A SPECIFIC ONE
    // array.splice(index, howmany, item1, ....., itemX)
    deleteTask: function (index) {
      this.rowData.splice(index, 1);
    },
    addToTable: function () {
      // this.firstNameList.push(this.firstName);
      // this.firstName = "";
      // this.lastNameList.push(this.lastName);
      // this.lastName = "";
      // this.addressList.push(this.address);
      // this.address = "";

      var my_object = {
        firstName: this.firstName,
        lastName: this.lastName,
        address: this.address,
        colorCheckbox: false,
      };

      this.rowData.push(my_object);
      this.firstName = "";
      this.lastName = "";
      this.address = "";
    },
  },
};
</script>
<style>
.redNotActive {
  color: rgb(0, 0, 0);
}

.redActive {
  color: rgb(241, 32, 0);
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

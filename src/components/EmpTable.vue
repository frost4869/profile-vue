<template>
  <div id="emp-table">
    <table>
      <thead>
        <tr>
          <th>No</th>
          <th>Name</th>
          <th>Email</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in data" :key="item.id">
          <td>{{item.id}}</td>
          <td>{{item.name}}</td>
          <td>{{item.email}}</td>
          <td>
            <button class="delete" v-on:click="deleteEmp(item.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "emp-table",
  props: {
    data: Array
  },
  methods: {
    deleteEmp(id) {
      this.$emit("remove:emp", id);
    }
  }
};
</script>

<style scoped>
.delete {
  background-color: #bf0000;
  color: #fff;
}
</style>
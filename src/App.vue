<template>
  <div id="app" class="small-container">
    <h1>Employees</h1>
    <emp-form @add:emp="addEmp" />
    <emp-table v-bind:data="employees" @remove:emp="removeEmp" />
  </div>
</template>

<script>
import EmpTable from "./components/EmpTable";
import EmpForm from "./components/EmpForm";
export default {
  name: "app",
  components: {
    EmpTable,
    EmpForm
  },
  data: () => {
    return {
      employees: [
        { id: 1, name: "something", email: "something@mail.com" },
        { id: 2, name: "batman", email: "batman123@mail.com" },
        { id: 3, name: "sups", email: "superm123@mail.com" }
      ]
    };
  },
  methods: {
    addEmp(employee) {
      const latestEmp = this.employees[this.employees.length - 1];
      const newEmp = {
        id: latestEmp.id + 1,
        ...employee
      };
      this.employees = [...this.employees, newEmp];
    },
    removeEmp(id) {
      if (confirm("Wanna delete this emp ?")) {
        const indexToDelete = this.employees.findIndex(emp => emp.id === id);
        if (indexToDelete >= 0) {
          this.employees = this.employees.filter((_, i) => i !== indexToDelete);
        }
      }
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

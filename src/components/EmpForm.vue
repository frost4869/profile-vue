<template>
  <form id="emp-form" class="margin-bottom" @submit.prevent="handleSubmit">
    <label for="name">Name</label>
    <input
      name="name"
      type="text"
      v-model="employee.name"
      :class="{'has-error': isLoading && invalidName}"
      @focus="clearStatuses"
    />
    <label for="email">Email</label>
    <input
      name="email"
      type="text"
      v-model="employee.email"
      :class="{'has-error': isLoading && invalidEmail}"
    />
    <p v-if="error && isLoading" class="error-message">Please fill all required fields</p>
    <p v-if="success" class="success-message">Success !</p>
    <button>Add new Emp</button>
  </form>
</template>

<script>
export default {
  name: "emp-form",
  data: () => {
    return {
      isLoading: false,
      error: false,
      success: false,
      employee: {
        name: "",
        email: ""
      }
    };
  },
  methods: {
    handleSubmit() {
      this.isLoading = true;
      this.clearStatuses();
      if (this.invalidName || this.invalidEmail) {
        this.error = true;
        return;
      }
      this.$emit("add:emp", this.employee);
      this.employee = {
        name: "",
        email: ""
      };
      this.error = false;
      this.success = true;
      this.isLoading = false;
    },
    clearStatuses() {
      this.error = false;
      this.success = false;
    }
  },
  computed: {
    invalidName() {
      return this.employee.name === "";
    },
    invalidEmail() {
      return this.employee.email === "";
    }
  }
};
</script>

<style scoped>
.error-message {
  color: #bf0000;
}
.success-message {
  color: #00a72a;
}
</style>
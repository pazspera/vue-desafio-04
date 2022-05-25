<template>
  <div>
    <h2>Create an account</h2>
    <input type="text" placeholder="email" v-model="email" />
    <input type="password" placeholder="password" v-model="password.password" />
    <input type="password" placeholder="confirm password" v-model="password.confirm" />
    <button @click.prevent="submitForm">Submit</button>
  </div>
</template>

<script>
import useValidate from "@vuelidate/core";
import { required } from "@vuelidate/validators";

export default {
  name: "VuelidateTest",
  setup() {
    return { v$: useValidate() };
  },
  data() {
    return {
      // Add vuelidate to component
     /*  v$: useValidate(), */
      email: "",
      password: {
        password: "",
        confirm: "",
      },
    };
  },
  validations() {
    return {
      // Uses the same structure as data
      email: { required },
      password: {
        password: { required },
        confirm: { required },
      },
    };
  },
  methods: {
    submitForm() {
      this.v$.validate();
      if (!this.v$.$error) {
        alert("Form Submitted");
      } else {
        alert("Form failed validation");
      }
    },
  },
};
</script>

<style></style>

<template>
  <div>
    <h2>Vuelidate Test 2</h2>
    <p><a href="https://vuelidate-next.netlify.app/">https://vuelidate-next.netlify.app/</a></p>

    <input type="text" name="firstName" id="firstName" placeholder="firstName">
    <br>
    <input type="text" name="lastName" id="lastName" placeholder="lastName">
    <br>
    <input type="email" name="email" id="email" placeholder="email">
    <br>
    <input type="submit" value="Submit">
  </div>
</template>

<script>
import useVuelidate from "@vuelidate/core";
import { required, email } from "@vuelidate/validators";

export default {
  setup() {
    return { v$: useVuelidate() };
  },
  data() {
    return {
      firstName: "",
      lastName: "",
      contact: {
        email: "",
      },
    };
  },
  validations() {
    return {
      firstName: { required }, // Matches this.firstName
      lastName: { required }, // Matches this.lastName
      contact: {
        email: { required, email }, // Matches this.contact.email
      },
    };
  },
};
</script>

<style></style>

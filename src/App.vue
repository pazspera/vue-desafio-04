<template>
  <div id="app">
    <FormWeb @submit-form="addUser" />
    <div class="my-5"></div>
    <TableUsers :users="users" />
  </div>
</template>

<script>
import FormWeb from "@/components/FormWeb.vue";
import TableUsers from "@/components/TableUsers.vue";

export default {
  name: "App",
  components: {
    FormWeb,
    TableUsers,
  },
  data() {
    return {
      users: [],
    };
  },
  methods: {
    addUser(formData) {
      const newUser = { ...formData };
      console.log(newUser);
      this.users.push(newUser);
    },
  },
};
</script>

<style>
#app {
  margin: 3rem 0;
}
</style>

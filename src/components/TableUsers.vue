<template>
  <div class="container">
    <div class="row">
      <div class="col">
        <table class="table">
          <thead>
            <tr>
              <th scope="col">Nombre</th>
              <th scope="col">Edad</th>
              <th scope="col">Email</th>
              <th scope="col">Cursos</th>
            </tr>
          </thead>
          <tbody>
              <tr v-for="user in users" :key="user.email">
                  <td>{{ user.name }}</td>
                  <td>{{ user.age }}</td>
                  <td>{{ user.email }}</td>
                  <td>{{ user.selectedCourses.join(', ') }}</td>
              </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TableUsers",
  props: {
      users: {
          type: Array,
          required: true
      }
  }
};
</script>

<style></style>

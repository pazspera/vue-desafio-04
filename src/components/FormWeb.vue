<template>
  <div class="container">
    <form @submit.prevent="submitForm">
      <!-- Nombre -->
      <div class="row mb-3">
        <div class="col">
          <label for="name" class="form-label">Nombre</label>
          <input type="text" class="form-control" name="Name" v-model="form.name" />
          <p>Nombre: {{ form.name }}</p>
        </div>
      </div>
      <!-- Edad -->
      <div class="row mb-3">
        <div class="col">
          <label for="age" class="form-label">Edad</label>
          <input type="number" name="age" class="form-control" v-model="form.age" />
          <p>Edad: {{ form.age }}</p>
        </div>
      </div>
      <!-- Email -->
      <div class="row mb-3">
        <div class="col">
          <label for="email" class="form-label">Email</label>
          <input type="email" name="email" class="form-control" v-model="form.email" />
          <p>Email: {{ form.email }}</p>
        </div>
      </div>
      <!-- Cursos -->
      <div class="row mb-3">
        <div class="col">
          <p class="form-label">Cursos disponibles</p>
          <div class="form-check" v-for="course in availableCourses" :key="course.id" :value="course.name">
            <input class="form-check-input" type="checkbox" :value="course.name" :id="course.id" v-model="form.selectedCourses" />
            <label :for="course.id" class="form-check-label">{{ course.name }}</label>
          </div>
          <p>Cursos seleccionados: {{ form.selectedCourses }}</p>
        </div>
      </div>
      <!-- Submit -->
      <button type="submit" class="btn btn-primary">Enviar</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "FormWeb",
  data() {
    return {
      availableCourses: [
        {
          id: "checkJavascript",
          name: "JavaScript",
        },
        {
          id: "checkVue",
          name: "Vue",
        },
        {
          id: "checkReact",
          name: "React",
        },
        {
          id: "checkAngular",
          name: "Angular",
        },
        {
          id: "checkNode",
          name: "NodeJS",
        },
      ],
      form: {
        name: "",
        age: 0,
        email: "",
        selectedCourses: [],
      },
    };
  },
  methods: {
      submitForm() {
          this.$emit("submit-form", {
              name: this.form.name,
              age: this.form.age,
              email: this.form.email,
              selectedCourses: this.form.selectedCourses,
          });

          console.log(this.form.name);
          console.log(this.form.age);
          console.log(this.form.email);
          console.log(this.form.selectedCourses);
      }
  }
};
</script>

<style></style>

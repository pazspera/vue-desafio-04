<template>
  <div class="container">
    <form @submit.prevent="submitForm">
      <!-- Nombre -->
      <div class="row mb-3">
        <div class="col">
          <label for="name" class="form-label">Nombre</label>
          <input type="text" class="form-control" name="Name" v-model="form.name" />
          <p>Nombre: {{ form.name }}</p>
          <p v-if="$v.form.name.$invalid" class="text-danger">El nombre es un campo requerido</p>
        </div>
      </div>
      <!-- Edad -->
      <div class="row mb-3">
        <div class="col">
          <label for="age" class="form-label">Edad</label>
          <input type="number" name="age" class="form-control" v-model="form.age" />
          <p>Edad: {{ form.age }}</p>
          <p v-if="$v.form.age.$invalid" class="text-danger">La edad ingresada es inválida</p>
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
      <button :disabled="$v.form.$invalid" type="submit" class="btn btn-primary">Enviar</button>
    </form>
  </div>
</template>

<script>
import useVuelidate from "@vuelidate/core";
import { required, integer, between } from "vuelidate/lib/validators";

export default {
  name: "FormWeb",
  setup() {
    return { v$: useVuelidate() };
  },
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
  validations: {
    form: {
      name: {
        required: required,
      },
      age: {
        required: required,
        integer: integer,
        between: between(18, 120),
      },
    },
  },
  methods: {
    submitForm() {
      if (!this.$v.form.$invalid) {
        this.$emit("submit-form", {
          name: this.form.name,
          age: this.form.age,
          email: this.form.email,
          selectedCourses: this.form.selectedCourses,
        });
      } else {
        console.log("Invalid form");
      }
    },
  },
};
</script>

<style></style>

<template>
  <div class="container">
    <form @submit.prevent="submitForm" autocomplete="off">
      <!-- Nombre -->
      <div class="row mb-3">
        <div class="col">
          <label for="name" class="form-label">Nombre</label>
          <input type="text" class="form-control" name="Name" v-model.trim="form.name" />
          <p v-if="$v.form.name.$invalid" class="text-danger">El nombre es requerido</p>
          <p class="text-success" v-else>El valor ingresado es correcto</p>
        </div>
      </div>
      <!-- Edad -->
      <div class="row mb-3">
        <div class="col">
          <label for="age" class="form-label">Edad</label>
          <input type="number" name="age" class="form-control" v-model.trim="form.age" />
          <p v-if="$v.form.age.$invalid" class="text-danger">La edad es requerida</p>
          <p class="text-success" v-else>El valor ingresado es correcto</p>
        </div>
      </div>
      <!-- Email -->
      <div class="row mb-3">
        <div class="col">
          <label for="email" class="form-label">Email</label>
          <input type="email" name="email" class="form-control" v-model="form.email" />
          <p v-if="$v.form.email.$invalid" class="text-danger">El email es requerido</p>
          <p class="text-success" v-else>El valor ingresado es correcto</p>
        </div>
      </div>
      <!-- Cursos -->
      <div class="row mb-3">
        <div class="col">
          <p class="form-label">Cursos disponibles</p>
          <div class="form-check" v-for="course in availableCourses" :key="course.id" :value="course.name">
            <input class="form-check-input" type="checkbox" :value="course.name" :id="course.id" v-model.number="form.selectedCourses" />
            <label :for="course.id" class="form-check-label">{{ course.name }}</label>
          </div>
          <p v-if="$v.form.selectedCourses.$invalid" class="text-danger">Seleccione al menos un curso</p>
          <p class="text-success" v-else>El valor ingresado es correcto</p>
        </div>
      </div>
      <!-- Submit -->
      <button :disabled="$v.form.$invalid" type="submit" class="btn btn-primary">Enviar</button>
    </form>
  </div>
</template>

<script>
import { required, integer, between, email } from "vuelidate/lib/validators";

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
  validations: {
    form: {
      name: {
        required,
      },
      age: {
        required,
        integer,
        between: between(18, 120),
      },
      email: {
        required,
        email,
      },
      selectedCourses: {
        required,
      },
    },
  },
  methods: {
    capitalize(value) {
      return value.replace(/\b\w/g, (l) => l.toUpperCase());
    },
    resetForm() {
      this.form.name = "";
      this.form.age = 0;
      this.form.email = "";
      this.form.selectedCourses = [];
    },
    submitForm() {
      if (!this.$v.form.$invalid) {
        this.$emit("submit-form", {
          name: this.capitalize(this.form.name),
          age: this.form.age,
          email: this.form.email.toLowerCase(),
          selectedCourses: this.form.selectedCourses,
        });
        this.$v.$reset();
        this.resetForm();
      } else {
        console.log("invalid form");
      }
    },
  },
};
</script>

<style></style>

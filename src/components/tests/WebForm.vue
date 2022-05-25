<template>
  <div>
    <div class="container">
      <form @submit.prevent="validateForm">
        <!-- Nombre y apellido -->
        <div class="row mb-3">
          <div class="col">
            <label class="form-label" for="firstName">Nombre</label>
            <input type="text" class="form-control" name="firstName" id="firstName" v-model="form.firstName" />
            <p>Nombre: {{ form.firstName }}</p>
          </div>
          <div class="col">
            <label class="form-label" for="lastName">Apellido</label>
            <input type="text" class="form-control" name="lastName" id="lastName" v-model="form.lastName" />
            <p>Apellido: {{ form.lastName }}</p>
          </div>
        </div>
        <!-- Email -->
        <div class="row mb-3">
          <div class="col">
            <label class="form-label" for="email">Email</label>
            <input class="form-control" type="email" name="email" id="email" v-model="form.email" />
            <p>Email: {{ form.email }}</p>
          </div>
        </div>
        <!-- País de residencia -->
        <div class="row mb-3">
          <div class="col">
            <p class="form-label">País de residencia</p>
            <select class="form-select" name="country" id="country" v-model="form.country">
              <option selected></option>
              <option v-for="country in countriesList" :key="country.id" :value="country.name">{{ country.name }}</option>
            </select>
            <p>País seleccionado: {{ form.country }}</p>
          </div>
        </div>
        <!-- Prueba checkboxes con v-for -->
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
        <!-- Comentarios -->
        <div class="row mb-3">
          <div class="col">
            <label for="comments" class="form-label">Comentarios</label>
            <textarea class="form-control" id="comments" rows="3" v-model="form.comments"></textarea>
            <p>Comentarios: {{ form.comments }}</p>
          </div>
        </div>
        <!-- Newsletter -->
        <div class="row mb-3">
          <div class="col">
            <div class="form-check">
              <input class="form-check-input" type="checkbox" name="newsletter" id="newsletter" v-model="form.newsletter" />
              <label class="form-check-label" for="newsletter">Suscribime al newsletter</label>
            </div>
            <p>Suscrito: {{ form.newsletter }}</p>
          </div>
        </div>
        <!-- Errores -->
        <div v-if="errors.length > 0">
          <p>Errores detectados:</p>
          <ul class="text-warning fw-bold">
            <li v-for="error in errors" v-bind:key="error.index">{{ error }}</li>
          </ul>
        </div>
        <!-- Submit -->
        <button type="submit" class="btn btn-primary">Enviar</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "WebForm",
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
      countriesList: [
        {
          id: "a",
          name: "Argentina",
        },
        {
          id: "b",
          name: "Uruguay",
        },
        {
          id: "c",
          name: "Chile",
        },
        {
          id: "d",
          name: "Perú",
        },
        {
          id: "e",
          name: "Mexico",
        },
      ],
      form: {
        firstName: "",
        lastName: "",
        email: "",
        country: "",
        selectedCourses: [],
        comments: "",
        newsletter: false,
      },
      errors: [],
    };
  },
  methods: {
    validateForm: () => {
      if (this.form.firstName && this.form.lastName && this.email) {
        return true;
      }
      if (this.form.firstName === "") {
        this.errors.push("El nombre es obligatorio.");
      }
      if (this.form.email === "") {
        this.errors.push("El correo electrónico es obligatorio.");
      }
      if (this.form.lastName === "") {
        this.errors.push("El apellido es obligatorio.");
      }
    },
  },
};
</script>

<style scoped>
.container {
  max-width: 650px;
}
</style>

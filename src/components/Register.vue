<template>
  <b-container>
    <div v-if="error" class="alert alert-danger">{{ error }}</div>

    <b-form @submit.prevent="submit">
      <b-form-group id="input-group-2" label="Nome:" label-for="input-2">
        <b-form-input
          id="reginput-2"
          v-model="form.name"
          required
          placeholder="Nome"
        ></b-form-input>
      </b-form-group>

      <b-form-group
        id="reginput-group-1"
        label="Email:"
        label-for="input-1"
        description="Nunca compartilhe seu email com ninguém!"
      >
        <b-form-input
          id="reginput-1"
          v-model="form.email"
          type="email"
          required
          placeholder="exemplo@exemplo.com"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="reginput-group-3" label="Senha:" label-for="reginput-3">
        <b-form-input
          id="reginput-3"
          v-model="form.password"
          type="password"
          required
          placeholder="Senha"
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Registrar</b-button>
    </b-form>
  </b-container>
</template>


<script>
import { FirebaseManager } from "../firebase/firebase";

export default {
  name: "Register",
  data() {
    return {
      form: {
        name: "",
        email: "",
        password: "",
      },
      error: null,
    };
  },
  methods: {
    submit() {
      FirebaseManager.registerUser(
        this.form.name,
        this.form.email,
        this.form.password,
        (response, result) => {
          if (response) {
            this.$router.push({ name: "CardBox" });
          } else {
            this.error = result;
          }
        }
      );
    },
  },
};
</script>
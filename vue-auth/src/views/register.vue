<template lang="pug">
.register
  .card.card-container
    Form(@submit="handleRegister" :validation-schema="schema")
      div(v-if="!successful")
        .form-group
          label(for="username") Username
          Field(name="username" type="text" class="form-control")
          ErrorMessage(name="username" class="error-feedback")

        .form-group
          label(for="email") Email
          Field(name="email" type="email" class="form-control")
          ErrorMessage(name="email" class="error-feedback")

        .form-group
          label(for="password") Password
          Field(name="password" type="password" class="form-control")
          ErrorMessage(name="password" class="error-feedback")


        .form-group
          button.btn.btn-primary.btn-block(:disabled="loading")
            span.spinner-border.spinner-border-sm(v-show="loading") 
            span Sign Up

      .alert(
        v-if="message"
        :class="successful ? 'alert-success' : 'alert-danger'"
      ) {{ message }}

  .card.card-container
    Person-constructor(:personaje="personaje" @personaje="(i) => personaje = JSON.stringify(i)")
    //- Person-constructor(:modelValue="personaje" @update:modelValue="n => personaje = n")

</template>

<script>
import { Form, Field, ErrorMessage } from "vee-validate";
import PersonConstructor from "../components/PersonConstructor.vue";
import * as yup from "yup";

export default {
  name: "Register",
  components: {
    Form,
    Field,
    PersonConstructor,
    ErrorMessage,
  },
  data() {
    const schema = yup.object().shape({
      username: yup
        .string()
        .required("Username is required!")
        .min(3, "Must be at least 3 characters!")
        .max(20, "Must be maximum 20 characters!"),
      email: yup
        .string()
        // .required("Email is required!")
        // .email("Email is invalid!")
        .max(50, "Must be maximum 50 characters!"),
      password: yup
        .string()
        .required("Password is required!")
        .min(6, "Must be at least 6 characters!")
        .max(40, "Must be maximum 40 characters!"),
    });

    // const personaje = `${
    //   (Math.floor(Math.random() * 11) + 1,
    //   Math.floor(Math.random() * 2) + 1,
    //   Math.floor(Math.random() * 11) + 1,
    //   Math.floor(Math.random() * 12) + 1)
    // }`;

    let personaje = null;

    return {
      successful: false,
      loading: false,
      message: "",
      personaje,
      schema,
    };
  },
  computed: {
    loggedIn() {
      return this.$store.state.auth.status.loggedIn;
    },
  },
  mounted() {
    if (this.loggedIn) {
      this.$router.push("/profile");
    }
  },
  methods: {
    handleLogin(user) {
      this.loading = true;

      this.$store.dispatch("auth/login", user).then(
        () => {
          this.$router.push("/profile");
        },
        (error) => {
          this.loading = false;
          this.message =
            (error.response &&
              error.response.data &&
              error.response.data.message) ||
            error.message ||
            error.toString();
        }
      );
    },

    handleRegister(user) {
      this.message = "";
      this.successful = false;
      this.loading = true;

      this.$store
        .dispatch("auth/register", { ...user, personaje: this.personaje })
        .then(
          (data) => {
            this.message = data.message;
            this.successful = true;
            this.loading = false;
            this.handleLogin(user);
          },
          (error) => {
            this.message =
              (error.response &&
                error.response.data &&
                error.response.data.message) ||
              error.message ||
              error.toString();
            this.successful = false;
            this.loading = false;
          }
        );
    },
  },
};
</script>

<style scoped>
label {
  display: block;
  margin-top: 10px;
}
.register {
  display: flex;
  align-items: stretch;
  margin: 50px auto;
  justify-content: center;
}

.card {
  max-width: 350px !important;
  padding: 40px 40px;
  background-color: #41414114;
  -moz-border-radius: 2px;
  -webkit-border-radius: 2px;
  border-radius: 2px;
  -moz-box-shadow: 0px 0px 20px 0px rgb(0 0 0 / 30%);
  -webkit-box-shadow: 0px 0px 20px 0px rgb(0 0 0 / 30%);
  box-shadow: 0px 0px 20px 0px rgb(0 0 0 / 30%);
}

.error-feedback {
  position: absolute;
  color: rgb(255, 0, 0);
  font-size: 10px;
}
</style>

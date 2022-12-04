<template lang="pug">
.test
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
            span.spinner-border.spinner-border-sm(v-show="loading") Sign Up

      .alert(
        v-if="message"
        :class="successful ? 'alert-success' : 'alert-danger'"
      ) {{ message }}

  .card.card-container
    Person-constructor(:personaje="personaje")
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
        .required("Email is required!")
        .email("Email is invalid!")
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

    const personaje = `10, 2, 3, 4`;

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
    handleRegister(user) {
      this.message = "";
      this.successful = false;
      this.loading = true;

      this.$store
        .dispatch("auth/register", { ...user, personaje: this.personaje })
        .then(
          (data) => {
            console.log(user, data);
            this.message = data.message;
            this.successful = true;
            this.loading = false;
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

.test {
  display: flex;
}

.card-container.card {
  max-width: 350px !important;
  padding: 40px 40px;
}

.card {
  background-color: #41414114;
  padding: 20px 25px 30px;
  margin: 0 auto 25px;
  margin-top: 50px;
  -moz-border-radius: 2px;
  -webkit-border-radius: 2px;
  border-radius: 2px;
  -moz-box-shadow: 0px 0px 20px 0px rgb(0 0 0 / 30%);
  -webkit-box-shadow: 0px 0px 20px 0px rgb(0 0 0 / 30%);
  box-shadow: 0px 0px 20px 0px rgb(0 0 0 / 30%);
}

.profile-img-card {
  width: 96px;
  height: 96px;
  margin: 0 auto 10px;
  display: block;
  -moz-border-radius: 50%;
  -webkit-border-radius: 50%;
  border-radius: 50%;
}

.error-feedback {
  color: red;
}
</style>

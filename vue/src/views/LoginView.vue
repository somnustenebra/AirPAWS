<template>
  <div id="login">
    <!-- Images for Login page -->
    <!-- <img id='paper-plane' src="@/assets/images/paper_plane.gif" alt="Paper Plane"> -->
    <img id="logo" src="@/assets/images/AirPAWS_Official_Logo.png" alt="AirPAWS Logo" />
    <img id="airplane" src="@/assets/images/paper_airplane_login.png" alt="Airplane Background" />
    <img id="cat" src="@/assets/images/cat_right_login2.png" alt="Cat" />
    <img id="dog" src="@/assets/images/dog_left_login.png" alt="Dog" />

    <div id="flavor-text">
      <h1>Welcome to AirPAWS!
        <p>Where furry companions <br> are always welcomed!</p>
      </h1>
    </div>

    <form v-on:submit.prevent="login">
      <h1>Please Sign In</h1>
      <div role="alert" v-if="invalidCredentials">
        Invalid username and password!
      </div>
      <div role="alert" v-if="this.$route.query.registration">
        Thank you for registering, please sign in.
      </div>
      <div class="form-input-group">
        <label for="username">Username</label>
        <input type="text" id="username" v-model="user.username" required autofocus />
      </div>
      <div class="form-input-group">
        <label for="password">Password</label>
        <input type="password" id="password" v-model="user.password" required />
      </div>
      <button type="submit">Sign in</button>
      <p>
        <router-link v-bind:to="{ name: 'register' }">Need an account? Sign up.</router-link>
      </p>
    </form>

  </div>
</template>

<script>
import authService from "../services/AuthService";
import "@/assets/login.css";

export default {
  components: {},
  data() {
    return {
      user: {
        username: "",
        password: ""
      },
      invalidCredentials: false
    };
  },
  methods: {
    login() {
      authService
        .login(this.user)
        .then(response => {
          if (response.status == 200) {
            this.$store.commit("SET_AUTH_TOKEN", response.data.token);
            this.$store.commit("SET_USER", response.data.user);
            this.$router.push("/");
          }
        })
        .catch(error => {
          const response = error.response;

          if (response.status === 401) {
            this.invalidCredentials = true;
          }
        });
    }
  }
};
</script>

<style scoped>
.form-input-group {
  margin-bottom: 1rem;
}

label {
  margin-right: 0.5rem;
}
</style>
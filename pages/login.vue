<template>
  <div class="container">
    <form @submit.prevent="login">
      <div class="is-size-4 has-text-centered" style=" padding-bottom:10px">Login</div>

      <div class="field">
        <p class="control has-icons-left has-icons-right">
          <input class="input" type="email" placeholder="Email" v-model="loginForm.email" />
          <span class="icon is-small is-left">
            <i class="fas fa-envelope"></i>
          </span>
          <span class="icon is-small is-right">
            <i class="fas fa-check"></i>
          </span>
        </p>
      </div>
      <div class="field">
        <p class="control has-icons-left">
          <input class="input" type="password" placeholder="Password" v-model="loginForm.password" />
          <span class="icon is-small is-left">
            <i class="fas fa-lock"></i>
          </span>
        </p>
      </div>
      <div class="field">
        <p class="control">
          <button class="button is-success">Register</button>
        </p>
      </div>
    </form>
  </div>
</template>
<script>
export default {
  layout: "auth",
  data() {
    return {
      loginForm: { email: "", password: "" }
    };
  },
  methods: {
    async login() {
      try {
        await this.$store.dispatch("auth/login", this.loginForm);
        this.$router.push("/");
      } catch (error) {
        console.log({ error });
      }
    }
  }
};
</script>

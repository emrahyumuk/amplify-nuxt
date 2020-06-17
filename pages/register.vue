<template>
  <div class="container">
    <form v-if="step === steps.register" @submit.prevent="register">
      <div class="is-size-4 has-text-centered" style=" padding-bottom:10px">Register</div>

      <div class="field">
        <p class="control has-icons-left has-icons-right">
          <input class="input" type="email" placeholder="Email" v-model="registerForm.email" />
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
          <input
            class="input"
            type="password"
            placeholder="Password"
            v-model="registerForm.password"
          />
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
    <form v-else @submit.prevent="confirm">
      <div class="is-size-4 has-text-centered" style=" padding-bottom:10px">Confirm</div>

      <div class="field">
        <p class="control has-icons-left has-icons-right">
          <input class="input" type="email" placeholder="Email" v-model="confirmForm.email" />
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
          <input class="input" type="text" placeholder="Code" v-model="confirmForm.code" />
          <span class="icon is-small is-left">
            <i class="fas fa-lock"></i>
          </span>
        </p>
      </div>
      <div class="field">
        <p class="control">
          <button class="button is-success">Confirm</button>
        </p>
      </div>
    </form>
    <nuxt-link to="/login">Have you account? Login</nuxt-link>
  </div>
</template>

<script>
const steps = {
  register: "REGISTER",
  confirm: "CONFIRM"
};
export default {
  layout: "auth",
  data() {
    return {
      steps: { ...steps },
      step: steps.register,
      registerForm: { email: "", password: "" },
      confirmForm: { email: "", code: "" }
    };
  },
  methods: {
    async register() {
      try {
        await this.$store.dispatch("auth/register", this.registerForm);
        this.confirmForm.email = this.registerForm.email;
        this.step = this.steps.confirm;
      } catch (error) {
        console.log({ error });
      }
    },
    async confirm() {
      try {
        await this.$store.dispatch(
          "auth/confirmRegistration",
          this.confirmForm
        );
        await this.$store.dispatch("auth/login", this.registerForm);
        this.$router.push("/");
      } catch (error) {
        console.log({ error });
      }
    }
  }
};
</script>

<template>
  <div>
    <div class="navbar header has-shadow is-primary" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <a class="navbar-item" href="/">
          <img src="~assets/buefy.png" alt="Buefy" height="28" />
        </a>

        <div class="navbar-burger">
          <span />
          <span />
          <span />
        </div>
      </div>
      <div class="navbar-end">
        <div v-if="!$auth.isAuthenticated" class="navbar-item">
          <div class="buttons">
            <nuxt-link class="button is-primary" to="/register">
              <strong>Sign up</strong>
            </nuxt-link>
            <nuxt-link class="button is-light" to="/login">Log in</nuxt-link>
          </div>
        </div>

        <div v-else class="navbar-item">
          <div class="buttons">
            <a class="navbar-item">{{$auth.email}}</a>

            <a class="button is-primary" @click="$store.dispatch('auth/logout')">
              <strong>Logout</strong>
            </a>
          </div>
        </div>
      </div>
    </div>

    <section class="main-content columns">
      <div class="column is-2 section">
        <p class="menu-label is-hidden-touch">General</p>
        <ul class="menu-list">
          <li v-for="(item, key) of items" :key="key">
            <nuxt-link :to="item.to" exact-active-class="is-active">
              <b-icon :icon="item.icon" />
              {{ item.title }}
            </nuxt-link>
          </li>
        </ul>
      </div>

      <div class="container column is-10">
        <nuxt />
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          title: "Home",
          icon: "home",
          to: { name: "index" }
        },
        {
          title: "Inspire",
          icon: "lightbulb",
          to: { name: "inspire" }
        }
      ]
    };
  },
  mounted() {
    console.log(this.$auth.user);
  }
};
</script>

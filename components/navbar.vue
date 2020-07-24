<template>
  <vs-navbar
    target-scroll="#padding-scroll-content"
    text-white
    color="dark"
    padding-scroll
    center-collapsed
    v-model="active"
  >
    <template #left>
      <img src="/main.svg" alt="" />
    </template>
    <vs-navbar-item :active="active == 'home'" id="home" to="/">
      Home
    </vs-navbar-item>
    <vs-navbar-item :active="active == 'about'" id="about" to="/about">
      About
    </vs-navbar-item>
    <vs-navbar-item
      v-if="$auth.loggedIn"
      :active="active == 'dafuq'"
      id="dafuq"
      to="/dafuq"
    >
      dafuq
    </vs-navbar-item>
    <template #right>
      <vs-button v-if="$auth.loggedIn" @click="logout"
        ><i class="bx bx-log-out"></i>&nbsp;Logout</vs-button
      >
      <vs-button v-else @click="google"
        ><i class="bx bx-log-in"></i>&nbsp;Login</vs-button
      >
    </template>
  </vs-navbar>
</template>
<script>
export default {
  data: () => ({
    active: "home",
  }),
  methods: {
    async google() {
      await this.$auth.loginWith("google").catch((e) => {
        console.log("Error" + e);
      });
    },
    async logout() {
      window.location.reload(true);
      await this.$auth.logout().catch((e) => {
        console.log("Error" + e);
      });
    },
  },
};
</script>

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
    <vs-navbar-item :active="active == 'dafuq'" id="dafuq" to="/dafuq">
      dafuq
    </vs-navbar-item>
    <template #right>
      <vs-button v-if="$auth.loggedIn"
        ><i class="bx bx-log-out"></i>&nbsp;Logout</vs-button
      >
      <vs-button v-else><i class="bx bx-log-in"></i>&nbsp;Login</vs-button>
      <vs-button v-if="!$auth.loggedIn"
        ><i class="bx bx-user-plus"></i>&nbsp;Register</vs-button
      >
    </template>
  </vs-navbar>
</template>
<script>
export default {
  data: () => ({
    active: "home",
  }),
};
</script>

<template>
  <div>
    <vs-navbar
      target-scroll="#padding-scroll-content"
      text-white
      color="dark"
      padding-scroll
      center-collapsed
      v-model="active"
      class="condensed"
    >
      <template #left>
        <img v-if="!$device.isMobile" src="/main.svg" alt="" />
        &nbsp;
        <vs-button
          v-if="$device.isMobile"
          @click="activeSidebar = !activeSidebar"
        >
          <i class="bx bx-menu"></i>
        </vs-button>
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
        <vs-button
          v-if="$auth.loggedIn"
          :animate-inactive="successFace"
          @click="handleClickFace"
          :loading="loadingFace"
          ><i class="bx bx-log-out"></i>&nbsp;Logout
          <template #animate>Really?</template>
        </vs-button>
        <vs-button v-else @click="google"
          ><i class="bx bx-log-in"></i>&nbsp;Login</vs-button
        >
      </template>
    </vs-navbar>
    <vs-sidebar
      absolute
      v-model="active"
      :open.sync="activeSidebar"
      background="dark"
      textWhite
    >
      <template #logo>
        <img src="/main.svg" alt="" />
      </template>
      <vs-sidebar-item id="home" :active="active == 'home'" to="/">
        <template #icon>
          <i class="bx bx-home"></i>
        </template>
        Home
      </vs-sidebar-item>
      <vs-sidebar-item :active="active == 'about'" id="about" to="/about">
        <template #icon>
          <i class="bx bx-label"></i>
        </template>
        About
      </vs-sidebar-item>
      <vs-sidebar-item
        v-if="$auth.loggedIn"
        :active="active == 'dafuq'"
        id="dafuq"
        to="/dafuq"
        ><template #icon>
          <i class="bx bx-question-mark"></i>
        </template>
        dafuq
      </vs-sidebar-item>
    </vs-sidebar>
  </div>
</template>
<script>
export default {
  data: () => ({
    active: "home",
    activeSidebar: false,
    loadingFace: false,
    successFace: false,
  }),
  methods: {
    async google() {
      await this.$auth.loginWith("google").catch((e) => {
        console.log("Error" + e);
      });
    },
    async handleClickFace() {
      this.loadingFace = true;
      setTimeout(() => {
        this.loadingFace = false;
        this.successFace = !this.successFace;
        this.$auth.logout().catch((e) => {
          console.log("Error" + e);
        });
        window.location.reload(true);
      }, 2000);
    },
  },
};
</script>
<style>
button {
  font-family: "IBM Plex Sans Condensed", sans-serif;
}
</style>

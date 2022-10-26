<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark ps-0 pe-0">
    <div class="container-fluid">
      <router-link class="navbar-brand" href="#" to="/home">
        <img src="../assets/logo.png" width="30" height="30" class="d-inline-block align-top" alt="" />
        Mark Analyzer
      </router-link>
      <button class="navbar-toggler fs-6" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDropdown"
        aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavDropdown">
        <ul class="navbar-nav">
          <router-link class="nav-item" to="/analyzer"><a class="nav-link" href="#">Analyzer</a></router-link>
          <router-link class="nav-item" to="/users"><a class="nav-link" href="#">Users</a></router-link>
        </ul>
      </div>
      <div class="collapse navbar-collapse" id="navbarNavDropdown">
        <ul class="navbar-nav ms-auto">
          <router-link class="nav-item" to="/"><a class="nav-link" href="#"><img :src="user ? user.avatar : null"
                class="avatar me-1" referrerpolicy="no-referrer">{{
                    user ? user.name : ""
                }}</a></router-link>
          <li class="nav-item">
            <a class="nav-link" aria-current="page" @click="this.$store.dispatch('logout')"
              style="cursor: pointer">Logout</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>

</template>

<script>
import store from "../store";
import { useStore } from "vuex";
export default {
  data() {
    return {
      store: useStore(),
      user: store.getters.getCurrentUser,
    };
  },
  watch: {
    user: function () {
      if (!this.user) this.$router.push("/");
    },
  },
  methods: {
  },
};
</script>

<style>
.nav-item {
  text-decoration: none !important;
}
</style>

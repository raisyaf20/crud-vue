<template>
  <navbar-comp />
  <router-view />
</template>

<script>
import NavbarComp from "@/components/Navbar.vue";
export default {
  components: {
    NavbarComp,
  },
};
</script>

<style>
#app {
  color: #2c3e50;
}
.color {
  color: #42b983;
}

/* nav a.router-link-exact-active {
  color: #42b983;
} */
</style>

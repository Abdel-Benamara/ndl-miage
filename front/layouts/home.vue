<template>
  <v-app>
    <navbar-sidebar></navbar-sidebar>
    <nuxt v-if="!isMobile"/>
    <v-main v-else>
      <v-container>
        <nuxt/>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import NavbarSidebar from "~/components/NavbarSidebar";
export default {
  name: "home",
  components: {NavbarSidebar},

  data : () => ({
    isMobile: false,
  }),

  mounted() {
    this.isMobile = /iPhone|iPad|iPod|Android/i.test(navigator.userAgent);
  },
}
</script>

<style scoped>

</style>

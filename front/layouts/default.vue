<template>
  <v-app dark>
    <navbar-sidebar></navbar-sidebar>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import NavbarSidebar from "~/components/NavbarSidebar";
export default {
  components: {NavbarSidebar}
}
</script>

<style scoped>

</style>

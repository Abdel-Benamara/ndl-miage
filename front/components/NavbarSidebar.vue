<template>
  <div>
    <v-navigation-drawer
      v-model="drawer"
      app
      absolute
      temporary
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon color="#034750">{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title color="#034750" v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title>
          <img src="~/assets/images/logo.png" width="60"/>
      </v-toolbar-title>
      <v-toolbar-title v-text="title">
      </v-toolbar-title>

      <v-spacer></v-spacer>

        <v-btn large text v-for="(item, index) in items" :key="index" v-if="!isMobile" color="#034750" @click="redirect(item.to)">
          {{item.title}}
        </v-btn>
    </v-app-bar>
  </div>
</template>

<script>
export default {
  name : "NavbarSidebar",
  data () {
    return {
      displayDropdown: true,
      username: "steeven alliel",
      clipped: true,
      drawer: false,
      fixed: false,
      isMobile: null,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Home',
          to: '/'
        },
        {
          icon: 'mdi-database-plus',
          title: 'Data Gathering',
          to: '/data-gathering'
        },
        {
          icon: 'mdi-account-group',
          title: 'About Us',
          to: '/about-us'
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: "418 I'm a Teapot"
    }
  },
  mounted() {
    this.isMobile = /iPhone|iPad|iPod|Android/i.test(navigator.userAgent);
  },

  methods: {

    redirect(to){
      this.$router.push(to)
    },
    sidebarMobile() {
      this.itemsSidebar.push(
        {
          icon: 'mdi-wifi',
          title: 'Connection WI-FI',
          to: '/',
        },
        {
          icon: 'mdi-office-building',
          title: 'Se Reperer dans la fac',
          to: '/',
        },
      )
    },

    afficherSidebar() {
      this.miniVariant = !this.miniVariant;
      if (this.isMobile) {
        this.miniVariant = false;
        this.drawer = !this.drawer
      }
    },


    async logout() {
      await this.$auth.logout()
    },

    redirectionProfil(index) {
      switch (index) {
        case 0 :
          this.$router.push('/profil');
          break;
        case 1:
          this.$toast.success('Deconnexion réussie');
          this.logout();
          break;

      }
    },
  },
  computed: {
    // ...mapGetters(['isAuthenticated', 'loggedInUser'])
  }
}
</script>

<style scoped>

.profil-dropdown {
  border: 2px solid white;
  border-top: none;
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;
}

.btn-dropdown-profil {
  border: 2px solid white;
}
.center {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>

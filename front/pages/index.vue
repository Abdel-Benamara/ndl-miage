<template>
  <div>
    <img src="~/assets/images/surfeur-banner-2.jpg" width="100%" height="60%"/>

    <v-container>
      <v-row justify="center" align="center">
        <v-col v-for="(item, index) in itemTab" :key="index" class="text-center">
            <v-container>
              <v-avatar
                color="#034750"
                width="150"
                height="150"
              >
                <v-icon dark size="80">{{item.icon}}</v-icon>
              </v-avatar>

              <h1 style="padding-top: 20px">{{item.title}}</h1>
            </v-container>
        </v-col>
      </v-row>
    </v-container>

    <v-row>
      <v-col class="text-center">
        <v-btn x-large outlined color="#034750">
          Rendez vous sur MyCity
          <v-icon></v-icon>
        </v-btn>
      </v-col>
    </v-row>
  </div>
</template>

<script>

export default {
  layout : "home",
  components: {
  },

  data: () => ({
    tabs: null,
    text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
    itemTab : [
      {
        icon : "mdi-weather-partly-snowy-rainy",
        title : "31°C",
        text : "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor",

      },
      {
        icon : "mdi-windsock",
        title: "10 Km/h",
        text : "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor",
      },
      {
        icon : "mdi-waves",
        text : "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor",
        title: "2,5 m",
      }
    ],
  }),
}
</script>

<style scoped>

</style>

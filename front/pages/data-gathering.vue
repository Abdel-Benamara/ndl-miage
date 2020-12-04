<template>
  <div>

      <div class="center">
        <img src="~/assets/images/logo.png" width="8%" />
      </div>

    <h2 class="text-center">Partagez nous votre journée surfeur·euse·s !</h2>

    <v-row justify="center" >
      <v-col cols="8" sm="8" md="10" lg="5" xl="5">
        <p class="text-center">
          Nous recueillons ces données dans le but d’améliorer votre expérience en mer.
          Ces informations resteront en notre possession et ne seront pas partagées avec des tiers.
        </p>
      </v-col>
    </v-row>

    <v-row justify="center" align="center">
      <v-col cols="12" sm="12" md="10" lg="8" xl="8">
        <v-card class="border">
            <v-container>
              <v-row>
                <v-col
                  v-for="(data, index) in nameData" :key="index"
                  cols="12" sm="12" md="6" lg="6" xl="6"
                >
                  <v-text-field
                    v-model="data.value"
                    :label="data.label"
                    required
                    color="#034750"
                  ></v-text-field>
                </v-col>
              </v-row>

              <v-row>
                <v-col cols="12" sm="12" md="4" lg="4" xl="4">
                  <v-menu
                    ref="menu-date"
                    v-model="menu"
                    :close-on-content-click="false"
                    :return-value.sync="date"
                    transition="scale-transition"
                    offset-y
                    min-width="290px"
                  >
                    <template v-slot:activator="{ on, attrs }">
                      <v-text-field
                        v-model="date"
                        label="Date de l'activité"
                        prepend-icon="mdi-calendar"
                        readonly
                        v-bind="attrs"
                        v-on="on"
                        color="#034750"
                      ></v-text-field>
                    </template>
                    <v-date-picker
                      v-model="date"
                      no-title
                      scrollable
                      color="#034750"
                    >
                      <v-spacer></v-spacer>
                      <v-btn
                        text
                        color="#034750"
                        @click="menu = false"
                      >
                        Cancel
                      </v-btn>
                      <v-btn
                        text
                        color="#034750"
                        @click="$refs['menu-date'].save(date)"
                      >
                        OK
                      </v-btn>
                    </v-date-picker>
                  </v-menu>
                </v-col>
                <v-col
                  cols="12"
                  sm="12" md="4" lg="4" xl="4"
                >
                  <v-menu
                    ref="menu-1"
                    v-model="timeData[0].menu"
                    :close-on-content-click="false"
                    :nudge-right="40"
                    :return-value.sync="timeData[0].value"
                    transition="scale-transition"
                    offset-y
                    max-width="290px"
                    min-width="290px"
                  >
                    <template v-slot:activator="{ on, attrs }">
                      <v-text-field
                        v-model="timeData[0].value"
                        :label="timeData[0].label"
                        prepend-icon="mdi-clock-time-four-outline"
                        readonly
                        v-bind="attrs"
                        v-on="on"
                        color="#034750"
                      ></v-text-field>
                    </template>
                    <v-time-picker
                      no-title
                      v-if="timeData[0].menu"
                      v-model="timeData[0].value"
                      full-width
                      color="#034750"
                      @click:minute="$refs['menu-1'].save(timeData[0].value)"
                    ></v-time-picker>
                  </v-menu>
                </v-col>
                <v-col
                  cols="12"
                  sm="12" md="4" lg="4" xl="4"
                >
                  <v-menu
                    ref="menu-2"
                    v-model="timeData[1].menu"
                    :close-on-content-click="false"
                    :nudge-right="40"
                    :return-value.sync="timeData[1].value"
                    transition="scale-transition"
                    offset-y
                    max-width="290px"
                    min-width="290px"
                  >
                    <template v-slot:activator="{ on, attrs }">
                      <v-text-field
                        v-model="timeData[1].value"
                        :label="timeData[1].label"
                        prepend-icon="mdi-clock-time-four-outline"
                        readonly
                        v-bind="attrs"
                        v-on="on"
                        color="#034750"
                      ></v-text-field>
                    </template>
                    <v-time-picker
                      no-title
                      v-if="timeData[1].menu"
                      v-model="timeData[1].value"
                      full-width
                      color="#034750"
                      @click:minute="$refs['menu-2'].save(timeData[1].value)"
                    ></v-time-picker>
                  </v-menu>
                </v-col>
              </v-row>

              <v-row>
                <v-col
                  cols="12"
                  sm="12" md="4" lg="4" xl="4"
                  v-for="(data, index) in dataForms" :key="index"
                >
                  <v-text-field
                    color="#034750"
                    v-model="data.value"
                    :label="data.label"
                    required
                  ></v-text-field>
                </v-col>
              </v-row>

              <v-row align="center" justify="center">
                <v-col cols="12" sm="12" md="6" lg="6" xl="6">
                  <v-select
                    v-model="value"
                    :items="items"
                    item-text="label"
                    item-value="value"
                    attach
                    chips
                    label="Produits utilisés dans la journée"
                    multiple
                    color="#034750"
                  ></v-select>
                </v-col>
                <v-col cols="12" sm="12" md="6" lg="6" xl="6">
                  <v-text-field
                    v-model="autre"
                    label="Autre produit"
                    required
                    color="#034750"
                  ></v-text-field>
                </v-col>
              </v-row>
            </v-container>

          <v-card-actions>
             <v-row align="center" justify="center">
               <v-col cols="3">
                 <v-btn x-large block dark color="#034750" @click="submit">
                   Valider
                 </v-btn>
               </v-col>
             </v-row>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  name: "data-gathering",

  data : () => ({
    valid: false,
    nameData : [
      {
        value : null,
        label : "Nom",
        field : "nom",
      },
      {
        value : null,
        label : "Prenom",
        field : "prenom",
      },
    ],
    date: new Date().toISOString().substr(0, 10),
    menu: false,
    timeData : [
      {
        menu : false,
        value : null,
        label : "Heure de début d'activtité",
        field : "heureDebut",
      },
      {
        menu : false,
        value : null,
        label : "Heure de fin d'activtité",
        field : "heureFin",
      },
    ],
    dataForms : [
      {
        value : null,
        label : "Ville",
        field : "ville",
      },
      {
        value : null,
        label : "Spot",
        field : "spot",
      },
      {
        value : null,
        label : "Nombre de surfeurs dans le groupe",
        field : "nbSurfers",
      },
    ],
    items: [
      { label: 'Crème solaire', value: 'cremeSolaire' },
      { label: 'Parfum / Déodorant', value: 'parfumDeodorant' },
      { label: 'Crème hydratante', value: 'cremeHydratante' },
      { label: 'Maquillage', value: 'maquillage' },
      { label: 'Essence', value: 'essence' },
      { label: 'Cigarette', value: 'cigarette' },
      { label: 'Engrais / Pesticides', value: 'engraisPesticides' },
      { label: 'Peintures', value: 'peintures' },
    ],
    value: [],
    autre : "",
  }),

  methods : {
    async submit(){

      const data = {};

      this.nameData.map(key => data[key.field] = key.value);
      this.timeData.map(key => data[key.field] = key.value);
      this.dataForms.map(key => data[key.field] = key.value);

      data.date = this.date;

      data.autre = this.autre;

      this.value.map(key => data[key] = true);

      await this.$axios({
        method : "post",
        url :"/data-gathering/add/data",
        data
      }).catch(e => {
        this.$toast.error("les données n'ont pas été ajoutées");
      });
      this.$toast.success("les données ont bien été ajoutées");
    }
  },
}
</script>

<style scoped>

.border{
  border: 2px solid #034750;
}

.center {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>

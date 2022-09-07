<template>
  <v-container>
    <v-card>
      <v-card-title>
        <v-text-field
          v-model="search"
          append-icon="mdi-magnify"
          label="Search"
          single-line
          hide-details
        ></v-text-field>
      </v-card-title>
      <v-data-table :headers="headers" :items="countries" :search="search">
        <template v-slot:[`item.actions`]="{ item }">
          <v-icon medium class="mr-2" @click="countryInfo(item)">
            mdi-information
          </v-icon>
        </template>
      </v-data-table>
    </v-card>
    <v-dialog
      v-model="dialog"
      fullscreen
      transition="dialog-bottom-transition"
      hide-overlay
    >
      <v-card>
        <v-toolbar dark color="primary">
          <v-btn icon dark @click="close">
            <v-icon>mdi-close</v-icon>
          </v-btn>
          <v-toolbar-title>{{ selectedCountry.Country }}</v-toolbar-title>
          <v-spacer></v-spacer>
        </v-toolbar>

        <v-card-text>
          <v-container>
            <v-card>
              <v-data-table :headers="headersInfo" :items="historyCases">
              </v-data-table>
            </v-card>
          </v-container>
        </v-card-text>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
import axios from "axios";
export default {
  name: "AllCountries",
  props: ["countries"],

  data() {
    return {
      search: "",
      items: [],
      dialog: false,
      headers: [
        {
          text: "Country",
          align: "start",
          filterable: true,
          value: "Country",
        },
        { text: "New Confirmed", value: "NewConfirmed" },
        { text: "Total Confirmed", value: "TotalConfirmed" },
        { text: "New Deaths", value: "NewDeaths" },
        { text: "New Recovered", value: "NewRecovered" },
        { text: "Total Recovered", value: "TotalRecovered" },
        { text: "Info", value: "actions", sortable: false },
      ],
      headersInfo: [
        {
          text: "New Confirmed",
          align: "start",
          filterable: true,
          value: "Active",
        },
        { text: "New Recovered", value: "Recovered", filterable: true },
        { text: "New Deaths", value: "Deaths", filterable: true },
        { text: "Date", value: "Date", filterable: true },
      ],
      selectedCountry: "",
      historyCases: [],
    };
  },

  methods: {
    countryInfo(item) {
      this.dialog = true;
      this.selectedCountry = item;
      this.getCountryCases(item.Slug);
    },
    close() {
      this.selectedCountry = "";
      this.dialog = false;
    },
    getCountryCases(slug) {
      axios
        .get(`https://api.covid19api.com/live/country/${slug}/status/confirmed`)
        .then((res) => {
          this.historyCases = res.data.map((item) => {
            return { ...item, Date: item.Date.split("T", 1) };
          });
        })
        .catch((error) => {
          console.log(error, "Doslo je do greske");
        });
    },
  },
};
</script>

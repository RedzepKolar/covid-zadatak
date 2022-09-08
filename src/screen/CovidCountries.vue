<template>
  <v-container>
      <v-card class="d-flex card-fix mx-auto">
      <cu-card cTitle="New Confirmed" :cData="globalData.NewConfirmed" />
      <cu-card cTitle="Total Confirmed" :cData="globalData.TotalConfirmed" />
      <cu-card cTitle="New Deaths" :cData="globalData.NewDeaths" />
    </v-card>
    <all-countries :countries="countries" />
  </v-container>
</template>

<script>
import axios from "axios";
import AllCountries from "@/components/AllCountries.vue";
import CustomCard from "@/components/CustomCard.vue";

export default {
  name: "CovidCountries",
  components: {
    "cu-card": CustomCard,
    "all-countries": AllCountries,
  },

  data: () => ({
    countries: [],
    globalData: null,
  }),
  methods: {
    getData() {
      axios
        .get("https://api.covid19api.com/summary")
        .then((res) => {
          this.countries = res.data.Countries;
          this.globalData = res.data.Global;
        })
        .catch((error) => {
          console.log(error, "Doslo je do greske");
        });
    },
  },
  created() {
    this.getData();
  },
};
</script>

<style>
  .card-fix {
    width: 98.8%;
  }

</style>
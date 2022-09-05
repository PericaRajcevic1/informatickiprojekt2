<template>
  <v-container>
    <h4 style="font-size: 2rem" class="text-center">  Poredak vozača {{ season }} </h4>


    <v-row no-gutters v-if="loaded" justify="center">
      <DriverCard
          v-for="(driver, idx) in drivers"
          :key="idx"
          class="driver"
          :class="driver.Constructors[0].constructorId"
          :driver="driver"
          :season="season"
      >
      </DriverCard>
    </v-row>
    <v-row no-gutters justify="center" v-else>
      <v-skeleton-loader
          v-for="i in 20"
          :key="i"
          class="pa-1"
          width="500"
          type="card">
      </v-skeleton-loader>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";
import DriverCard from "@/components/DriverCard";

export default {
  name: "Home",
  components: {DriverCard},
  data() {
    return {
      loaded: false,
      drivers: null,
      season: ''
    }
  },
  mounted() {
    axios
        .get('https://ergast.com/api/f1/2022/driverStandings.json', {
          
        })
        .then((response) => {
          this.season = response.data.MRData.StandingsTable.season
          this.drivers = response.data.MRData.StandingsTable.StandingsLists[0].DriverStandings
        })
        .finally(() => (this.loaded = true))


  },
}

</script>

<style scoped>

</style>

<template>

  <v-container
      id="mycontainer"
  >


    <v-row justify="center">
      <v-col cols="12" md="6">


        <v-card elevation="6" rounded="lg" class="mt-2 pa-3 " v-if="!nextRaceLoading">

          <v-row justify="space-around">
            <v-card-title class="d-flex flex-column">
              <h2>
                Sljedeća utrka
              </h2>

              <h4 class="text-break text-center">
                {{ nextRace[0].raceName }} @ {{ nextRace[0].Circuit.circuitName }}
              </h4>

              <v-chip outlined>
                {{
                  new Date(nextRace[0].date).toLocaleDateString("en-DE", {
                    year: "numeric",
                    month: "long",
                    day: "numeric"
                  })
                }}
                ({{ nextRace[0].time.slice(0, -4) }} UTC)
              </v-chip>

            </v-card-title>

          </v-row>


          <v-row justify="space-around">
            <vac :end-time="new Date(nextRaceTimeDate).getTime() ">
              <template
                  v-slot:process="{ timeObj }">

                <v-chip-group>
                  <v-chip :x-large="$vuetify.breakpoint.smAndUp"><span
                      v-text="timeObj.d > 1 ? timeObj.d + ' dana' : timeObj.d +' day' "/></v-chip>
                  <v-chip :x-large="$vuetify.breakpoint.smAndUp">{{ `${timeObj.h}` }} sati</v-chip>
                  <v-chip :x-large="$vuetify.breakpoint.smAndUp">{{ `${timeObj.m}` }} minuta</v-chip>
                  <v-chip :x-large="$vuetify.breakpoint.smAndUp" color="primary">{{ `${timeObj.s}` }} sekundi</v-chip>
                </v-chip-group>

              </template>
              <template
                  v-slot:finish>
                <span>Utrka je u toku!</span>
              </template>
            </vac>
          </v-row>
        </v-card>
      </v-col>

    </v-row>
    <v-row justify="space-between">
      <v-col cols="12" md="8">
        <ResultCard title="Poredak prošle utrke" :last-race="lastRace" :loading="loading"
                    :results="results.slice(0,limit)"/>
        <v-row class="mt-4" justify="center">
          <v-btn color="primary" rounded outlined v-if="limit<20" @click="limit=20">Učitaj više...</v-btn>
        </v-row>
      </v-col>
      <v-col cols="12" md="4">
        <v-card height="840" class="overflow-auto mt-8 pa-3">
          <Timeline id="f1" sourceType="profile" />
        </v-card>
      </v-col>

    </v-row>



  </v-container>

</template>

<script>
import axios from "axios";
import ResultCard from "@/components/ResultCard";
import {Timeline} from 'vue-tweet-embed'

export default {
  name: "Home",
  components: {ResultCard, Timeline},
  data() {
    return {
      loading: true,
      nextRaceLoading: true,
      lastRace: [],
      nextRace: null,
      nextRaceTime: '',
      nextRaceTimeDate: '',
      results: [],
      limit: 13,
      headers: [
        {text: 'Pos.', value: 'position', align: 'start', sortable: false},
        {text: 'Driver', value: 'Driver.familyName'},
        {text: 'Constructor', value: 'Constructor.name'},
        {text: 'Pts.', value: 'points'},
      ]
    }
  },


  mounted() {
    this.getLastResults()
    this.getNextRace()
    this.getStatus()
  },
  methods: {
    getStatus() {
      return "Time.time"
    },
    getLastResults() {
      axios
          .get('https://ergast.com/api/f1/current/last/results.json', {
            
          })
          .then((response) => {
            this.loading = false
            this.lastRace = response.data.MRData.RaceTable.Races[0]
            this.results = response.data.MRData.RaceTable.Races[0].Results
          });
    },
    getNextRace() {
      axios
          .get('https://ergast.com/api/f1/current/next.json', {
            
          })
          .then((response) => {
            this.nextRaceLoading = false
            this.nextRace = response.data.MRData.RaceTable.Races
            this.nextRaceTimeDate = this.nextRaceTime.concat(
                this.nextRace[0].date, 'T', this.nextRace[0].time
            );

          });
    },
  }

}


</script>

<style scoped>


#customTitle {
  letter-spacing: 10px;
}
</style>

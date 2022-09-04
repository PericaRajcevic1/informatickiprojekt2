<template>
  <div>
    <v-navigation-drawer
        app
        floating
        class="rounded-lg"
        :class='{ "my-4": $vuetify.breakpoint.mdAndUp, "my-2": $vuetify.breakpoint.smAndDown, "mx-4": $vuetify.breakpoint.mdAndUp && drawer, "mx-2": $vuetify.breakpoint.smAndDown && drawer }'
        overlay-opacity=".75"
        v-model="drawer"
        :width='$vuetify.breakpoint.smAndDown ? 310 : 360'
        :height='`calc(100vh - ${$vuetify.breakpoint.smAndDown ? "16" : "32"}px)`'
        temporary
        color="secondary"
        dark
    >

      <v-list
          nav
      >

        <v-list-item-group
            v-model="group"
            active-class="gray"
        >
          <v-list-item to="/">
            <v-list-item-icon>
              <v-icon>mdi-home</v-icon>
            </v-list-item-icon>

            <v-list-item-content>
              <v-list-item-title>Početna</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-divider></v-divider>

          <v-list-item
              v-for="(item, i) in items"
              :key="i"
              :to="item.route"
          >


            <v-list-item-icon>
              <v-icon v-text="item.icon"></v-icon>
            </v-list-item-icon>

            <v-list-item-content>
              <v-list-item-title v-text="item.text"></v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-divider></v-divider>

          <v-list-item to="/news">
            <v-list-item-icon>
              <v-icon>mdi-newspaper</v-icon>
            </v-list-item-icon>

            <v-list-item-content>
              <v-list-item-title>F1 Vijesti</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>

      </v-list>
      <v-list-item-group active-class="primary">

      </v-list-item-group>

     
    </v-navigation-drawer>

    <v-app-bar
        app
        flat
    >

      <v-app-bar-nav-icon aria-label="Nav button" @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
     

      <v-toolbar-title id="title--f1">F1 INFO</v-toolbar-title>

      <v-spacer/>
      <div v-if="$vuetify.breakpoint.lgAndUp">

          <v-btn aria-label="Početna" fab small to="/" class="ml-4" text rounded active-class="primary">
            <v-icon>mdi-home</v-icon>
          </v-btn>
          <v-btn
              v-for="(item, i) in items"
              :key="i"
              :to="item.route"
              text
              active-class="primary"
              class="ml-4"

          >
            <v-icon left>{{item.icon}}</v-icon>
            {{ item.text }}
          </v-btn>
      </div>

      <v-spacer></v-spacer>

      <v-btn aria-label="Promjena teme" icon @click="$vuetify.theme.dark = !$vuetify.theme.dark">

        <v-icon>
          {{ $vuetify.theme.dark ? "mdi-white-balance-sunny" : "mdi-brightness-3" }}
        </v-icon>

      </v-btn>

    </v-app-bar>


  </div>
</template>
<script>
export default {
  data: () => ({
    drawer: false,
    group: null,
    selectedItem: 0,
    items: [
      {text: 'Poredak vozača', icon: 'mdi-racing-helmet', route: '/driverStandings'},
      {text: 'Poredak konstruktora', icon: 'mdi-car-sports', route: '/constructorStandings'},
      {text: 'Kalendar', icon: 'mdi-calendar', route: '/calendar'},
      {text: 'Pretraga Sezona', icon: 'mdi-calendar-multiple', route: '/seasons'},
    ],
  }),
  watch: {
    group() {
      this.drawer = false
    },
  },
}
</script>
<style>
#title--f1 {
  /*font-family: "Grenze", sans-serif;*/
  font-size: 2.5rem;
  font-weight: bold;
  color: #FF385C;
}
</style>

<template>

  <v-app>

    <!--    appBar & navDrawer-->
    <AppNavDrawer/>

    <!--main view / router-->
    <v-main>
        <router-view></router-view>
    </v-main>

    

  </v-app>

</template>

<script>
import AppNavDrawer from "@/components/AppNavDrawer";

export default {
  name: 'App',
  components: {
    AppNavDrawer
  },


}
</script>
<style>
@import './assets/styles/styles.css';
</style>

<template>

  <v-app>

    <!--    appBar i navDrawer-->
    <AppNavDrawer/>
    
    <!--main view / router-->
    <v-main>
        <router-view></router-view>
    </v-main>
    
    <br>

    <Footer/>

  </v-app>


  

</template>

<script>
import AppNavDrawer from "@/components/AppNavDrawer";
import Footer from "@/components/Footer";

export default {
  name: 'App',
  components: {
    AppNavDrawer,
    Footer
  },


}
</script>
<style>
@import './assets/styles/styles.css';
</style>

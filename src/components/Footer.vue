<template>
    <v-footer
      dark
      padless
    >
      <v-card
        class="flex"
        flat
        tile
        
      >
        
    
    <v-card-title class="justify-center">
          
        <v-btn class="mx-4" dark icon @click="toFacebook()">
          <v-icon size="24px">mdi-facebook</v-icon>
        </v-btn>

        <v-btn class="mx-4" dark icon @click="toInstagram()">
          <v-icon size="24px">mdi-instagram</v-icon>
        </v-btn>

        <v-btn class="mx-4" dark icon @click="toTwitter()">
          <v-icon size="24px">mdi-twitter</v-icon>
        </v-btn>

       
    </v-card-title>
        <v-card-text class="py-2 white--text text-center">
          {{ new Date().getFullYear() }} @ <strong>Perica Rajčević</strong>
        </v-card-text>
      </v-card>
    </v-footer>
  </template>

<script>
    export default {
      data: () => ({
        icons: [
          'mdi-facebook',
          'mdi-twitter',
          'mdi-instagram',
        ],
      }),
      methods: {
      toFacebook: function(){
        window.open('https://www.facebook.com/pericarajcevic00/')
      },
       toInstagram: function(){
        window.open('https://www.instagram.com/perica.rajcevic/')
      },
       toTwitter: function(){
        window.open('https://twitter.com/PekiBmw')
      },
      
    }
    }
  </script>
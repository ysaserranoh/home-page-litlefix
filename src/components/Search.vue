<template>
  <v-layout column fill-height class="black pt-2">
    <v-flex xs12>
      <v-layout row wrap>
        <v-flex xs2>
          <v-btn icon dark @click.native="$emit('close')">
            <v-icon >close</v-icon>
          </v-btn>
        </v-flex>
        <v-flex xs10 mt-2 pt-1 text-xs-left v-if="$vuetify.breakpoint.mdAndDown">
          <img src="../assets/liteflix.svg">
        </v-flex>
      </v-layout>
      <v-layout row wrap px-4>
        <v-flex xs1 pt-2>
           <img src="../assets/lupa.svg">
        </v-flex>
        <v-flex xs11 style="margin-top: -10px;">
          <v-text-field dark lass="style-font ml-1" label="Titulos, géneros, personas" single-line hide-details></v-text-field>
        </v-flex>
      </v-layout>
    </v-flex>
  </v-layout>
</template>
<style scoped>
  >>> .v-text-field .v-label {
    font-size: 14px;
    color: #4A4A4A;
    margin-top: 0px;
  }

  .style-font {
   color: #999999;
  }
</style>

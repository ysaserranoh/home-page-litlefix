<template>
  <v-app>
    <v-content id="app">
    <Toolbars app></Toolbars>
      <v-container black fill-height fluid pa-0 ma-0>
        <router-view style="margin-top: -70px; margin-bottom: 30px;"/>
      </v-container>
    </v-content>
    <Footer app style="margin-bottom: 90px;"></Footer>
  </v-app>
</template>
<script>
import Toolbars from '@/components/Toolbars'
import Footer from '@/components/Footer'

export default {
  components: { Toolbars, Footer }
}
</script>
<style>
  #app{
    background-color: black;
  }
</style>

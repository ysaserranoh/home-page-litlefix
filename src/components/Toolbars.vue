<template>
  <v-layout row wrap>
    <v-toolbar color="transparent" flat height="40">
      <v-flex xs12 mt-3 v-if="$vuetify.breakpoint.mdAndDown">
        <!--Mobile-->
        <v-layout row wrap align-center justify-left>
          <v-flex xs1>
            <v-toolbar-side-icon dark  @click="drawer = !drawer"></v-toolbar-side-icon>
          </v-flex>
          <v-flex xs9 text-xs-center v-if="$vuetify.breakpoint.mdAndDown">
            <img src="../assets/liteflix.svg">
          </v-flex>
          <v-flex xs1>
             <v-btn @click="searchMobile = !searchMobile" color="white" small fab flat>
              <img src="../assets/lupa.svg">
            </v-btn>
          </v-flex>
        </v-layout>
      </v-flex>
      <v-spacer></v-spacer>
      <!--Section one toolbar-->
      <v-flex xs5 pt-4 v-if="$vuetify.breakpoint.mdAndUp">
        <v-toolbar-items>
          <div class="logo">
            <img src="../assets/liteflix.svg">
          </div>
          <v-list-tile class="mt-3">
            <v-list-tile-content>
              <v-list-tile-title class="body-1 white--text text-capitalize">Inicio</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-list-tile class="mt-3 margin-list">
            <v-list-tile-content>
              <v-list-tile-title class="body-1 white--text text-capitalize">Series</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-list-tile class="mt-3 margin-list">
            <v-list-tile-content>
              <v-list-tile-title class="body-1 white--text text-capitalize">Películas</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-list-tile class="mt-3 margin-list">
            <v-list-tile-content>
              <v-list-tile-title class="body-1 white--text text-none">Agregados recientemente</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-list-tile class="mt-3 margin-list">
            <v-list-tile-content>
              <v-list-tile-title class="body-1 white--text text-none">Mi lista</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-btn class="add-movies mt-4" style="margin-left: -5px" @click="add = !add" color="white" small fab flat>
            <v-icon medium style="margin-top: -10px">+</v-icon>
          </v-btn>
        </v-toolbar-items>
      </v-flex>
      <!--Section two toolbar-->
      <v-flex xs4 pt-4 v-if="$vuetify.breakpoint.mdAndUp">
        <v-toolbar-items style="margin-left: 0px">
          <v-layout row wrap>
            <!--Search Section-->
            <v-flex xs7>
              <v-spacer v-if="!search"></v-spacer>
                <v-list-tile class="mt-3">
                <v-layout>
                  <v-flex xs1 v-if="search">
                    <v-list-tile-content>
                     <img @click="search = !search" src="../assets/lupa.svg">
                    </v-list-tile-content>
                  </v-flex>
                  <v-flex xs11 style="margin-top: -10px;">
                    <v-text-field v-if="search" class="ml-1" label="Titulos, géneros, personas" single-line hide-details></v-text-field>
                  </v-flex>
                  <v-flex xs1 v-if="!search">
                    <v-list-tile-content>
                     <img @click="search = !search" src="../assets/lupa.svg">
                    </v-list-tile-content>
                  </v-flex>
                </v-layout>
              </v-list-tile>
            </v-flex>
            <v-flex xs3>
              <v-layout row wrap>
                <v-list-tile class="mt-3 margin-list_section-3">
                <v-list-tile-content>
                  <v-list-tile-title class="body-1 white--text font-weight-medium text-capitalize">Niños</v-list-tile-title>
                </v-list-tile-content>
              </v-list-tile>
              <v-list-tile class="mt-3 margin-list_section-3">
                <v-badge color="red" overlap right>
                  <span slot="badge"></span>
                  <v-list-tile-content>
                     <img src="../assets/bell.svg">
                  </v-list-tile-content>
                </v-badge>
              </v-list-tile>
              </v-layout>
            </v-flex>
            <v-flex xs2 v-if="$vuetify.breakpoint.mdAndUp">
             <v-menu offset-y bottom left class="mt-3" transition="slide-y-transition">
                <v-list slot="activator" class="mt-1" dark style="background-color: transparent;">
                  <img height="25" src="../assets/icon1.png">
                  <v-icon class="ml-2" medium>keyboard_arrow_down</v-icon>
                </v-list>
                <v-card class="diag-cont ml-5" flat style="width: 135px; border-radius: 5px; margin-top: 18px;">
                  <v-list subheader dense class="grey--text" v-for="(currentUser, index) in user" :key="index">
                    <v-list-tile avatar style="margin-top: -10px; margin-left: -5px; cursor: pointer;">
                      <v-list-tile-avatar>
                        <img :src="require('../assets/' + currentUser.image)">
                      </v-list-tile-avatar>
                      <v-list-tile-content style="margin-left: -15px">
                        <v-list-tile-title :class="currentUser.visited ? 'caption  black--text ' : 'caption'">{{ currentUser.name }}</v-list-tile-title>
                      </v-list-tile-content>
                    </v-list-tile>
                  </v-list>
                  <v-list class="" subheader dense>
                    <v-list-tile style="cursor: pointer;">
                     <v-list-tile-content>
                        <v-list-tile-title class="caption">Configuración</v-list-tile-title>
                      </v-list-tile-content>
                    </v-list-tile>
                   <v-divider class="mx-2"></v-divider>
                    <v-list-tile style="cursor: pointer;">
                       <v-list-tile-content>
                        <v-list-tile-title  class="caption">Ayuda</v-list-tile-title>
                      </v-list-tile-content>
                    </v-list-tile>
                    <v-divider class="mx-2"></v-divider>
                    <v-list-tile style="cursor: pointer;">
                      <v-list-tile-content>
                        <v-list-tile-title class="caption font-weight-bold ">Log Out</v-list-tile-title>
                      </v-list-tile-content>
                    </v-list-tile>
                  </v-list>
                </v-card>
              </v-menu>
            </v-flex>
          </v-layout>
        </v-toolbar-items>
      </v-flex>
      <v-spacer></v-spacer>
    </v-toolbar>
    <!--mobile-->
    <v-navigation-drawer persistent v-model="drawer" clipped fixed dark class="black" width="200" disable-resize-watcher>
      <v-list dense class="pt-0">
        <v-toolbar dark flat color="black" class="white--text">
          <v-list>
            <v-list-tile style="margin-left: -20px;">
              <v-toolbar-side-icon class="hidden-md-and-up" style="color:white" @click="drawer = !drawer"></v-toolbar-side-icon>
              <v-list-tile-title>
                <router-link to="/home" class="white--text" >
                    <img src="../assets/liteflix.svg">
                </router-link>
              </v-list-tile-title>
            </v-list-tile>
          </v-list>
        </v-toolbar>
        <div class="text-xs-left">
          <v-btn round class="text-capitalize caption  ml-3" style="width: 160px" color="grey darken-3" dark>
            <img style="margin-left: -80px" class="mr-1" width="30" src='../assets/icon2.png'>
            User 02
          </v-btn>
        </div>
        <v-list-tile style="cursor: pointer; margin-bottom: -5px">
         <v-list-tile-content>
            <v-list-tile-title class="caption">Cambiar usuario</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-divider class="mx-3"></v-divider>
          <v-list-tile style="cursor: pointer; margin-top: -10px; margin-bottom: -5px">
           <v-list-tile-content>
              <v-list-tile-title class="caption">Configuración</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        <v-divider class="mx-3"></v-divider>
        <v-list-tile style="cursor: pointer; margin-top: -10px; margin-bottom: -5px">
           <v-list-tile-content>
            <v-list-tile-title  class="caption">Ayuda</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-divider class="mx-3"></v-divider>
      </v-list>

      <v-list subheader dense>
        <v-list-tile style="cursor: pointer;">
         <v-list-tile-content>
            <v-list-tile-title class="caption">Series</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile style="cursor: pointer; margin-top: -10px">
           <v-list-tile-content>
            <v-list-tile-title  class="caption">Peliculas</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
         <v-list-tile style="cursor: pointer;margin-top: -10px">
           <v-list-tile-content>
            <v-list-tile-title  class="caption">Mi lista</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
         <v-list-tile style="cursor: pointer; margin-top: -10px">
           <v-list-tile-content>
            <v-list-tile-title class="caption">Niños</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>

        <div class="text-xs-left">
          <v-btn round class="add-movies-mobile text-capitalize caption  ml-3" style="width: 160px" color="red accent-4" dark>
            <v-icon medium class="mr-1" style="margin-left:-30px; margin-top: -10px">+</v-icon> Agregar película
          </v-btn>
        </div>

        <v-list-tile style="cursor: pointer;">
          <v-list-tile-content>
            <v-list-tile-title class="caption font-weight-bold ">Log Out</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-dialog v-model="add" width="730" transition="dialog-bottom-transition">
      <Add @close="add=false"></Add>
    </v-dialog>
    <v-dialog v-model="searchMobile" fullscreen transition="dialog-bottom-transition">
      <Search @close="searchMobile=false"></Search>
    </v-dialog>
  </v-layout>
</template>
<script>
import Add from '@/components/Add'
import Search from '@/components/Search'
export default {
  components: { Add, Search },
  data () {
    return {
      drawer: false,
      search: false,
      searchMobile: false,
      add: false,
      user: [
        { name: 'Ernesto Garmendia', image: 'icon2.png', visited: true },
        { name: 'User 03', image: 'icon3.png' },
        { name: 'User 04', image: 'icon3.png' }
      ]
    }
  }
}
</script>
<style scoped>
  >>> .v-dialog {
    border-radius: 10px;
  }
  .v-menu__content {
    -webkit-box-shadow: none;
    box-shadow: none;
    margin-top: -5px;
  }

  >>> .v-badge__badge {
    width: 8px;
    height: 8px;
    margin-top: 8px;
  }

  >>> .v-text-field .v-label {
    font-size: 14px;
    color: #4A4A4A;
    margin-top: 0px;
  }

  .add-movies {
    background-color: #e50914;
/*    padding: 20px;*/
  }

  .add-movies-mobile {
    background-color: #e50914;
  }

  .diag-cont:after {
    content: "";
    border-bottom: .70rem solid #ffff;
    border-left: .99rem solid transparent;
    border-right: .99rem solid transparent;
    position: absolute;
    top: -9px;
    left: 55%;
    z-index: 1000;
  }

  .logo{
    margin-top: 20px;
    margin-left: -40px;
  }

  .margin-list{
    margin-left: -20px;
    cursor: pointer;
  }

  .margin-list_section-3{
    margin-left: -10px;
    cursor: pointer;
  }
</style>

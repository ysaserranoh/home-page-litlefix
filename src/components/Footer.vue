<template>
  <v-footer dark height="300" fill-height class="black" inset>
    <v-layout row wrap fill-height align-center :class="$vuetify.breakpoint.smAndDown ? 'ml-0' : 'mt-5'">
      <v-flex md1></v-flex>
      <v-flex xs12 md11>
        <v-card tile class="black ma-0">
          <v-card-text style="margin-left: -10px">
            <v-hover v-for="icon in icons" :key="icon">
              <v-btn slot-scope="{ hover }" icon :color="hover ? 'red accent-4' : ''">
                <v-icon size="30px" :color="hover ? '' : 'grey lighten-1'">{{ icon }}</v-icon>
              </v-btn>
            </v-hover>
          </v-card-text>

          <v-card-text v-if="$vuetify.breakpoint.mdAndUp">
            <v-layout row wrap>
              <v-flex md3 class="style-font body-1">
                <div class="point white--text">Todos los titulos</div>
                <div class="point pt-2">Prensa</div>
                <div class="point pt-2">Confidencialidad</div>
                <div class="point pt-2">Contacto</div>
              </v-flex>
              <v-flex md3 class="style-font body-1">
                <div class="point">Cancelar Subscripción</div>
                <div class="point pt-2">Inversores</div>
                <div class="point pt-2">Legales</div>
              </v-flex>
              <v-flex md4 class="style-font body-1">
                <div class="point">Ayuda</div>
                <div class="point pt-2">RRHH</div>
                <div class="point pt-2">Cookies</div>
              </v-flex>
            </v-layout>
          </v-card-text>

          <v-card-text v-else>
            <v-layout row wrap>
              <v-flex xs8 md3 class="style-font body-1">
                <div class="point">Todos los titulos</div>
                <div class="point pt-2">Prensa</div>
                <div class="point pt-2">Confidencialidad</div>
                <div class="point pt-2">Contacto</div>
                <div class="point pt-2">Cancelar Subscripción</div>
              </v-flex>
              <v-flex xs4 class="style-font body-1 pl-2">
                <div class="point">Inversores</div>
                <div class="point pt-2">Legales</div>
                <div class="point pt-2">Ayuda</div>
                <div class="point pt-2">RRHH</div>
                <div class="point pt-2">Cookies</div>
              </v-flex>
            </v-layout>
          </v-card-text>

          <v-card-text class="style-font caption">
            &copy; 1997-2018 Liteflix, Inc.
          </v-card-text>
        </v-card>
      </v-flex>
  </v-layout>
  </v-footer>
</template>
<script>
export default {
  data: () => ({
    icons: [
      'fab fa-facebook-square',
      'fab fa-instagram',
      'fab fa-twitter',
      'fab fa-youtube'
    ]
  })
}
</script>
<style scoped>
.style-font {
 font-family: montserrat-regular;
 color: #999999;
}
.point{
  cursor: pointer;
}

</style>

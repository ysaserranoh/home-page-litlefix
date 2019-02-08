<template>
  <v-layout column fill-height class="pb-5">
    <v-flex xs12 :class="$vuetify.breakpoint.smAndDown ? 'wallpaper-mobile' : 'wallpaper'" style="min-height: 100vh;">
      <v-layout row wrap align-center justify-center pt-5 mt-5 :fill-height="$vuetify.breakpoint.smAndDown ? true : false">
        <v-flex md1></v-flex>
        <v-flex xs12 md11>
          <!--Wrapper-->
          <v-flex xs12 md4 :class="$vuetify.breakpoint.smAndDown ? 'pt-2' : 'ml-4 pt-5'">
            <div :class="$vuetify.breakpoint.smAndDown ? 'text-uppercase white--text style-font subheading text-xs-center' : 'text-uppercase white--text style-font headline'">
              Original de <span class="font-weight-black">Liteflix</span>
            </div>
            <div :class="$vuetify.breakpoint.smAndDown ? 'white--text style-font-center text-xs-center' : 'mt-2 white--text style-font-center'" :style="$vuetify.breakpoint.smAndDown ? 'font-size: 60px; line-height: 60px;' : 'font-size: 104px; line-height: 80px;'">Kids at school</div>
            <v-layout row class="mt-2" style="margin-left: -10px" :justify-center="$vuetify.breakpoint.smAndDown ? true : false">
              <v-btn round dark :style="$vuetify.breakpoint.smAndDown ? 'opacity: .7; width: 140px; height: 40px;' : ''" class="buttom-pl style-font text-capitalize">
                <v-icon :style="$vuetify.breakpoint.smAndDown ? 'margin-left: -15px' : 'margin-left: -35px'" class="pr-2 rotate-icon" dark>details</v-icon>
                <div style="margin-left: -15px">Reproducir</div>
              </v-btn>
              <v-btn v-if="$vuetify.breakpoint.mdAndUp" round dark class="buttom-pl style-font text-capitalize">
                <v-icon class="pr-2" style="margin-left: -70px" dark>add</v-icon>
               <div style="margin-left: -5px">Mi lista</div>
              </v-btn>
            </v-layout>
            <v-flex xs12 text-xs-right>
               <v-btn v-if="$vuetify.breakpoint.mdAndDown" outline style="width:30px; height: 30px; margin-top: -70px;" fab dark>
                <v-icon>add</v-icon>
              </v-btn>
            </v-flex>
            <div class="mt-0" v-if="$vuetify.breakpoint.mdAndUp">
              <div class="mt-3 white--text style-font subheading">Ver temporada 1</div>
              <div class="mt-2 white--text style-font" style="font-size: 14px;  text-align: justify">
               Lorem ipsum dolor amet chicharrones dreamcatcher hammock bushwick hell of, ethical 3 wolf moon
               celiac neutra mumblecore four dollar toast. Slow-carb post-ironic kickstarter synth franzen.
              </div>
            </div>
          </v-flex>
         </v-flex>
        <v-spacer></v-spacer>
      </v-layout>
    </v-flex>
    <v-layout row wrap fill-height align-center>
      <v-flex md1></v-flex>
      <v-flex xs11 md11 height>
        <Soon ref="soon" :config="config" :style="$vuetify.breakpoint.smAndDown ?  'margin-top: -80px;' : 'margin-top: -150px; margin-left: 10px'"></Soon>
        <Ranked ref="ranked" :config="config"></Ranked>
        <Popular ref="popular" :config="config"></Popular>
        <Drama ref="drama" :config="config"></Drama>
      </v-flex>
    </v-layout>
  </v-layout>
</template>
<script>
import Soon from '@/components/Soon'
import Ranked from '@/components/Ranked'
import Drama from '@/components/Drama'
import Popular from '@/components/Popular'
import axios from 'axios'

export default {
  components: { Soon, Ranked, Drama, Popular },
  data () {
    return {
      message: null,
      config: null,
      status: {
        ready: false
      }
    }
  },
  methods: {
    async getconfig () {
      this.status.ready = false

      let result = await axios.get('https://api.themoviedb.org/3/configuration?api_key=6f26fd536dd6192ec8a57e94141f8b20')
      this.config = result.data.images
      this.$nextTick(() => {
        this.$refs.soon.getImages()
        this.$refs.ranked.getImages()
        this.$refs.popular.getImages()
        this.$refs.drama.getImages()
      })
    }
  },
  created: function () {
    this.getconfig()
  }
}
</script>
<style scoped>
@font-face {
  font-family: American Typewriter Bold;
  src: url("../assets/fonts/American Typewriter Bold.ttf");
}

.wallpaper {
  background: url(../assets/wallpaper.jpg) no-repeat;
  background-size: cover;
}

.wallpaper-mobile {
  background: url(../assets/wallpaper.jpg) no-repeat center center;
  background-size: cover;
}

.style-font {
 font-family: montserrat-Regular;
}

.buttom-pl {
  width: 160px;
  height: 40px;
  opacity: .7;
}

.style-font-center {
  font-family: American Typewriter Bold;
}

.rotate-icon {
  transform: rotate(-90deg);
  transform-origin: 25% 65%;
}
</style>

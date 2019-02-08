<template>
  <v-flex>
    <div class="contain" :style="$vuetify.breakpoint.smAndDown ? 'min-height: 280px;' : 'min-height: 300px;'">
      <div class="row">
        <div class="style-font pb-2 mb-2 title white--text font-weight-bold">Próximamente</div>
        <div :class="$vuetify.breakpoint.smAndDown ? 'row__inner-mobile' :'row__inner'" v-if="ready">
          <!--card desktop-->
          <template v-if="$vuetify.breakpoint.mdAndUp">
            <div class="tile" v-for="(movies, index) in slider" :key="index">
            <div class="tile__media" v-for="(info, i) in infoSlider" :key="i">
              <v-layout
                column
                fill-heigth
                align-center
                class="tile__img"
                :style="{ backgroundImage: 'url(' + (config.secure_base_url + config.backdrop_sizes[0] + movies.backdrop_path) + ')' }"
              >
                <div class="tile__details" style="margin-top: -20px">
                  <v-flex class="tile__title" px-1 pt-0>
                    <v-flex xs12 text-xs-left px-0>
                      <v-btn outline class="mt-5" style="width:30px; height: 30px;" fab dark>
                        <v-icon small :style="$vuetify.breakpoint.smAndDown ? 'margin-left: -15px' : 'margin-left: 0px'" class="rotate-icon" dark>details</v-icon>
                      </v-btn>
                    </v-flex>
                    <v-flex xs12 px-2>
                      <div style="font-size: 10px; width: 143px;" class="style-font font-weight-bold white--text text-truncate">{{movies.title}}</div>
                      <v-layout row wrap>
                        <v-flex xs5>
                          <v-flex xs6 class="style-font-item style-font white--text">{{info.chance}}</v-flex>
                          <v-flex xs6 class="style-font-item style-font white--text">{{info.category}}</v-flex>
                        </v-flex>
                        <v-flex xs5 ml-2>
                          <v-layout row wrap>
                            <v-flex xs1>
                              <v-btn round fab dark class="style-font white--text vot">
                                 +16
                              </v-btn>
                            </v-flex>
                            <v-flex xs11 text-xs-left class="style-font-item  p-2 style-font white--text">
                              <div class="pl-3">1h 30 min</div>
                            </v-flex>
                          </v-layout>
                        </v-flex>
                        <v-flex xs1 text-xs-right>
                          <v-flex style="margin-top: -15px;">
                            <v-btn outline class="mt-2 button-action" fab dark>
                               <v-icon size="8" dark>far fa-thumbs-up</v-icon>
                            </v-btn>
                          </v-flex>
                          <v-flex>
                            <v-btn outline class="mt-0 button-action" fab dark>
                             <v-icon size="10" dark>add</v-icon>
                            </v-btn>
                          </v-flex>
                        </v-flex>
                      </v-layout>
                      <v-flex style="margin-top: -15px;" text-xs-center>
                        <v-btn class="mt-0 button-action" fab flat style="width:25px; height: 25px;" dark>
                         <v-icon medium dark>expand_more</v-icon>
                        </v-btn>
                      </v-flex>
                    </v-flex>
                  </v-flex>
                </div>
              </v-layout>
            </div>
          </div>
         </template>
          <!--Mobile-->
          <div v-if="$vuetify.breakpoint.mdAndDown" >
            <v-carousel hide-controls hide-delimiters height="150">
            <v-carousel-item>
              <div class="tile-mobile" v-for="(movies, index) in slider.slice(0, 6)" :key="index">
                <v-layout
                  column
                  fill-heigth
                  align-center
                  class="tile__img"
                  :style="{ backgroundImage: 'url(' + (config.secure_base_url + config.backdrop_sizes[0] + movies.backdrop_path) + ')' }"
                >
                </v-layout>
              </div>
            </v-carousel-item>
            <v-carousel-item>
              <div class="tile-mobile" v-for="(movies, index) in slider.slice(6, 12)" :key="index">
                <v-layout
                  column
                  fill-heigth
                  align-center
                  class="tile__img"
                  :style="{ backgroundImage: 'url(' + (config.secure_base_url + config.backdrop_sizes[0] + movies.backdrop_path) + ')' }"
                >
                </v-layout>
              </div>
            </v-carousel-item>
            <v-carousel-item>
              <div class="tile-mobile" v-for="(movies, index) in slider.slice(12, 18)" :key="index">
                <v-layout
                  column
                  fill-heigth
                  align-center
                  class="tile__img"
                  :style="{ backgroundImage: 'url(' + (config.secure_base_url + config.backdrop_sizes[0] + movies.backdrop_path) + ')' }"
                >
                </v-layout>
              </div>
            </v-carousel-item>
          </v-carousel>
          </div>
        </div>
      </div>
    </div>
  </v-flex>
</template>
<script>
import axios from 'axios'
export default {
  props: ['config'],
  data () {
    return {
      slider: [],
      infoSlider: [
        { chance: '98% Coincidencia', category: 'Suspenso', time: '1h 30 min' }
      ],
      message: null,
      ready: false,
      status: {
        loading: false,
        error: false,
        message: ''
      }
    }
  },
  methods: {
    async getImages () {
      let result = await axios.get('https://api.themoviedb.org/3/movie/upcoming?api_key=6f26fd536dd6192ec8a57e94141f8b20')
      if (result) {
        this.slider = result.data.results
        this.ready = true
      } else { }
    }
  }
}
</script>
<style scoped>
  >>> .theme--dark.v-btn:not(.v-btn--icon):not(.v-btn--flat) {
      background-color: #BDBDBD;
   }
  * {
    box-sizing: border-box;
  }
  h1,
  p {
    text-align: center;
  }
  p {
    width: 100%;
    max-width: 500px;
    margin: auto;
  }
  a:link,
  a:hover,
  a:active,
  a:visited {
    transition: color 150ms;
    color: #95a5a6;
    text-decoration: none;
  }

  a:hover {
    color: #7f8c8d;
    text-decoration: underline;
  }

  .contain {
   display: flex;
    flex-direction: row;
    flex-wrap: no-wrap;
    justify-content: center;
    align-items: center;
    overflow: hidden;
  }

  .row {
    width: 100%;
  }

  .row__inner {
    transition: 450ms -webkit-transform;
    transition: 450ms transform;
    transition: 450ms transform, 450ms -webkit-transform;
    font-size: 0;
    white-space: nowrap;
    padding-bottom: 10px;
  }

  .tile {
    position: relative;
    display: inline-block;
    width: 200px;
    height: 125px;
    margin-right: 10px;
    cursor: pointer;
    transition: 450ms all;
    -webkit-transform-origin: center left;
    transform-origin: center left;
  }

  .tile__img {
    width: 200px;
    height: 125px;
    -o-object-fit: cover;
    object-fit: cover;
    background-size: cover;
  }

  .tile__details {
    overflow: hidden;
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    top: 0;
    font-size: 10px;
    opacity: 0;
    background: linear-gradient(to top, rgba(0,0,0,0.9) 0%, rgba(0,0,0,0) 100%);
    transition: 450ms opacity;
  }

  .tile:hover .tile__details {
    opacity: 1;
  }

  .row__inner:hover .tile:hover {
    -webkit-transform: scale(2);
    transform: scale(2);
    opacity: 1;
  }
  .tile:hover ~ .tile {
    -webkit-transform: translate3d(140px, 0, 0);
    transform: translate3d(200px, 0, 0);
  }

  .style-font {
   font-family: montserrat-regular;
   color: #999999;
  }

  .style-font-item {
    font-family: montserrat-regular;
    color: #999999;
    font-size: 8px;
  }

  .rotate-icon {
    transform: rotate(-90deg);
  }

  .button-action {
    width:15px;
    height: 15px;
  }

  .vot {
    width:20px;
    height: 10px;
    font-size: 8px;
    opacity: .7;
    margin-top:2px;
    margin-left: -3px;
  }

  /*Mobile*/
  .row__inner-mobile {
    transition: 450ms -webkit-transform;
    transition: 450ms transform;
    transition: 450ms transform, 450ms -webkit-transform;
    font-size: 0;
    white-space: nowrap;
    padding-bottom: 10px;
  }

  .tile-mobile {
    position: relative;
    display: inline-block;
    width: 200px;
    height: 125px;
    margin-right: 10px;
    cursor: pointer;
    transition: 450ms all;
    -webkit-transform-origin: center left;
    transform-origin: center left;
  }

  .row__inner-mobile:hover .tile-mobile {
   /* opacity: 0.3;*/
  }

  .row__inner-mobile:hover .tile-mobile:hover {
    -webkit-transform: scale(1.1);
    transform: scale(1.1);
    opacity: 1;
  }

 .tile-mobile:hover ~ .tile-mobile {
    -webkit-transform: translate3d(50px, 0, 0);
    transform: translate3d(20px, 0, 0);
  }
</style>

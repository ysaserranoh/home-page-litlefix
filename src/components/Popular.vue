<template>
  <v-flex>
    <div class="contain">
      <div class="row" :class="$vuetify.breakpoint.smAndDown ? '' : ' mt-5'">
        <div class="style-font pb-3 mb-2 title white--text font-weight-bold">POPULARES DE LITEFLIX</div>
        <div class="row__inner" v-if="ready">
          <!--card>-->
          <div class="tile" v-for="(movies, index) in slider" :key="index">
            <div class="tile__media" v-for="(info, index) in infoSlider" :key="index">
              <v-layout
                column
                fill-heigth
                align-center
                class="tile__img"
                :style="{ backgroundImage: 'url(' + (config.secure_base_url + config.profile_sizes[2] + movies.backdrop_path) + ')' }"
              > <div class="tile__details mt-4 pt-3">
                  <v-flex class="tile__title" mt-5 pt-5>
                    <v-flex xs12 text-xs-left>
                      <v-btn outline class="mt-5" style="width:20px; height: 20px;" fab dark>
                        <v-icon size="12" :style="$vuetify.breakpoint.smAndDown ? 'margin-left: -15px' : 'margin-left: 2px;'" class=" rotate-icon" dark>details</v-icon>
                      </v-btn>
                    </v-flex>
                    <v-flex xs12 ml-2 mr-3>
                      <div class="style-font caption font-weight-bold white--text">{{info.title}}</div>
                      <v-layout row wrap>
                        <v-flex xs5>
                          <v-flex xs6 style="font-size: 10px" class=" style-font white--text">{{info.chance}}</v-flex>
                          <v-flex xs6 style="font-size: 10px" class=" style-font white--text">{{info.category}}</v-flex>
                          <v-flex xs5 ml-2>
                            <v-layout row wrap>
                              <v-flex xs1>
                                <v-btn round fab dark style="width:20px; height: 10px; font-size: 8px; opacity: .7; margin-top:2px; margin-left: -10px" class="style-font white--text">+16
                                </v-btn>
                              </v-flex>
                              <v-flex xs11 text-xs-left style="font-size: 8px; margin-top: 2px;" class="style-font white--text">
                                <div class="pl-3">1h 30 min</div>
                              </v-flex>
                            </v-layout>
                          </v-flex>
                        </v-flex>
                        <v-spacer></v-spacer>
                        <v-flex xs1 text-xs-right mr-2>
                          <v-flex style="margin-top: -15px;">
                            <v-btn outline class="mt-3" style="width:15px; height: 15px;" fab dark>
                               <v-icon size="8" dark>far fa-thumbs-up</v-icon>
                            </v-btn>
                          </v-flex>
                        </v-flex>
                      </v-layout>
                      <v-flex style="margin-top: -5px;" text-xs-center>
                        <v-btn class="mt-0" fab flat style="width:30px; height: 30px;" dark>
                         <v-icon light x-large>expand_more</v-icon>
                        </v-btn>
                      </v-flex>
                    </v-flex>
                  </v-flex>
                </div>
              </v-layout>
            </div>
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
      ready: false
    }
  },
  methods: {
    async getImages () {
      let result = await axios.get('https://api.themoviedb.org/3/movie/popular?api_key=6f26fd536dd6192ec8a57e94141f8b20')
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

  .contain {
   display: flex;
    flex-direction: row;
    flex-wrap: no-wrap;
    justify-content: center;
    align-items: center;
    min-height: 150px;
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
    width: 180px;
    height: 280px;
    margin-right: 10px;
    cursor: pointer;
    transition: 450ms all;
    -webkit-transform-origin: center left;
    transform-origin: center left;
  }

  .tile__img {
    width: 180px;
    height: 280px;
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
    /*.row__inner:hover {
      -webkit-transform: translate3d(-62.5px, 0, 0);
      transform: translate3d(-62.5px, 0, 0);
    }*/

  .row__inner:hover .tile {
    opacity: 0.3;
  }

  .row__inner:hover .tile:hover {
    -webkit-transform: scale(1.5);
    transform: scale(1.3);
    opacity: 1;
  }

  .tile:hover ~ .tile {
    -webkit-transform: translate3d(125px, 0, 0);
    transform: translate3d(55px, 0, 0);
  }

  .style-font {
    font-family: montserrat-regular;
    color: #999999;
  }

  .rotate-icon {
    transform: rotate(-90deg);
  }
</style>

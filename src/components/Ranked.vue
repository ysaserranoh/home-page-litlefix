<template>
  <div class="contain" :style="$vuetify.breakpoint.smAndDown ? 'margin-top: -50px' : ''">
    <div class="row">
      <div class="style-font pb-3 title mb-2 white--text font-weight-bold">Mejores Rankeadas</div>
      <div class="row__inner" v-if="ready">
        <v-carousel hide-controls hide-delimiters interval="4000" height="150">
          <v-carousel-item>
            <div class="tile" v-for="(movies, index) in slider.slice(0, 6)" :key="index">
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
            <div class="tile" v-for="(movies, index) in slider.slice(6, 12)" :key="index">
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
            <div class="tile" v-for="(movies, index) in slider.slice(12, 18)" :key="index">
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
</template>
<script>
import axios from 'axios'
export default {
  props: ['config'],
  data () {
    return {
      slider: [],
      ready: false
    }
  },
  methods: {
    async getImages () {
      let result = await axios.get('https://api.themoviedb.org/3/movie/top_rated?api_key=6f26fd536dd6192ec8a57e94141f8b20')
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
    min-height: 280px;
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
    height: 150px;
    margin-right: 10px;
    cursor: pointer;
    transition: 450ms all;
    -webkit-transform-origin: center left;
    transform-origin: center left;
  }

  .tile__img {
    width: 200px;
    height: 150px;
    -o-object-fit: cover;
    object-fit: cover;
    background-size: cover;
  }

  .row__inner:hover .tile {
    opacity: 0.3;
  }

  .row__inner:hover .tile:hover {
    -webkit-transform: scale(1.1);
    transform: scale(1.1);
    opacity: 1;
  }

  .tile:hover ~ .tile {
    -webkit-transform: translate3d(50px, 0, 0);
    transform: translate3d(20px, 0, 0);
  }

  .style-font {
   font-family: montserrat-regular;
   color: #999999;
  }

  .rotate-icon{
    transform: rotate(-90deg);
  }
</style>

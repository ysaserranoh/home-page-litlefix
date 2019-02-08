<template>
  <v-layout column fill-height class="white">
    <v-card style="min-height: 100px;" v-if="!congratulations">
      <v-flex xs12 pa-2 text-xs-right>
        <v-btn small icon @click.native="$emit('close')">
          <v-icon small>close</v-icon>
        </v-btn>
      </v-flex>
      <v-card-text>
        <v-container grid-list-md class="pa-0 px-3">
          <v-form ref="movieForm" v-model="valid" encType="multipart/form-data">
            <v-flex xs12 text-xs-center py-5 style="border: 1px dashed #9B9B9B; border-radius: 10px; cursor: pointer;" @click="onFocus">
              <div class="input-style">
                <v-layout row wrap>
                  <v-flex xs6 text-xs-right :class="$vuetify.breakpoint.mdAndDown ? 'primary--text caption' : 'primary--text'">
                    <v-icon class="rotate-icon pl-1 pt-0" color="primary">fas fa-link</v-icon>
                    <b>Agregar archivo</b>
                  </v-flex>
                  <v-flex xs6 text-xs-left  :class="$vuetify.breakpoint.mdAndDown ? 'caption' : ''" :style="$vuetify.breakpoint.mdAndDown ? 'margin-top: 7px; color: #9B9B9B;' : 'margin-top: 2px; color: #9B9B9B;'"> o arrastrarlo y soltarlo aquí</v-flex>
                </v-layout>

              </div>
               <input id="input" ref="fileInputImage" :rules="baseRules" type="file" style="display: none !important" accept="image/png, image/jpg" @change="encodeImageFileAsURL($event)"/>
            </v-flex>
            <v-layout row wrap pt-4>
              <v-flex xs12 sm6 md6 class="style-font text-uppercase">
                <div>Nombre de la Pelicula</div>
                <v-text-field :rules="baseRules" v-model="movie.title" style="margin-top: -10px"></v-text-field>
              </v-flex>

              <v-flex xs12 sm6 md6 class="style-font text-uppercase">
                <div>Categoria</div>
                <v-select :rules="Rules" v-model="movie.categoria" style="margin-top: -10px" :items="categoria"></v-select>
              </v-flex>
            </v-layout>
          </v-form>
        </v-container>
        <v-flex xs12 text-xs-center>
          <v-btn  @click.native="save"  dark round class="text-capitalize style-font subheading" :style="$vuetify.breakpoint.mdAndDown ? 'height: 60px; width: 200px; border-radius: 35px; background-color: #DEDEDE;' : 'height: 70px; width: 350px; border-radius: 35px; background-color: #DEDEDE;'">Subir Película</v-btn>
           <v-flex xs8>
            <v-alert v-if="status.show" style="height: 40px !important" :color="status.error ? 'error' : 'success'" :icon="status.error ? 'warning' : 'check'" value="true">{{status.message}}</v-alert>
          </v-flex>
        </v-flex>
      </v-card-text>
    </v-card>
    <v-card v-if="congratulations" style="min-height: 100px; background-color: #7ED321;">
      <v-card-text>
        <v-container grid-list-md class="px-3">
          <div class="logo">
            <img src="../assets/liteflix.svg">
          </div>
          <v-flex xs9 pt-4>
            <div class="style-font display-1 font-weight-medium white--text">Felicitaciones!</div>
            <div class="style-font headline white--text">
              <b>Liteflix The Movie</b> fue correctamente subido
              a la categoría <b>Aventuras</b>
            </div>
          </v-flex>
        </v-container>
         <v-flex xs12 text-xs-left pt-5>
            <v-btn dark round class="text-capitalize style-font subheading" style="height: 70px; width: 192px; border-radius: 35px; background-color: black;" @click.native="$emit('close'); congratulations=false; close()">Cerrar</v-btn>
          </v-flex>
      </v-card-text>
    </v-card>
  </v-layout>
</template>
<script>
export default {
  data () {
    return {
      formData: new FormData(),
      valid: false,
      congratulations: false,
      categoria: [
        'Acción',
        'Animación',
        'Aventuras',
        'Ciencia Ficción',
        'Comedia',
        'Documentales',
        'Drama'
      ],
      movies: [],
      movie: {
        title: '',
        image: '',
        categoria: ''
      },
      status: {
        show: false,
        loading: false,
        error: false,
        message: ''
      },
      baseRules: [
        (v) => !!v || 'Required.'
      ],
      Rules: [
        (v) => !!v || 'Este campo no puede estar vacío!',
        (v) => (v && v.length >= 1 && v.length <= 72) || 'La descripción debe tener menos de 72 caracteres!'
      ]
    }
  },
  methods: {
    async save () {
      this.status.loading = true
      this.status.error = false
      this.status.message = ''

      if (this.$refs.movieForm.validate()) {
        try {
          this.movies = this.getLocal()
          this.movies.push(this.movie)

          localStorage.setItem('movies', JSON.stringify(this.movies))
          this.status.loading = false
          this.status.error = false
          this.status.message = 'Se ha guardado la Película.'
          this.status.show = true
          this.congratulations = true
          this.$refs.movieForm.clear()
        } catch (error) {
          console.log(error)
          this.status.loading = false
          this.status.error = true
          this.status.message = 'Ha ocurrido un error.'
          this.status.show = true
        }
      } else {
        this.status.loading = false
        this.status.error = true
        this.status.message = 'Por favor ingrese los datos requeridos.'
        this.status.show = true
      }
    },

    encodeImageFileAsURL ($event) {
      let file = ($event.target.files || $event.dataTransfer.files)[0]
      let reader = new FileReader()
      reader.onloadend = () => {
        this.movie.image = reader.result
      }
      reader.readAsDataURL(file)
    },

    getLocal () {
      return JSON.parse(localStorage.getItem('movies')) || []
    },

    onFocus () {
      this.$refs.fileInputImage.click()
    },

    close () {
      this.movie = {
        title: '',
        image: '',
        categoria: ''
      }
      this.status = {
        show: false,
        loading: false,
        error: false,
        message: ''
      }
    }
  }
}
</script>
<style scoped>
  .style-font {
   font-family: montserrat-regular;
   color: #9B9B9B;
  }

  .input-style {
     font-family: montserrat-regular;
     font-size: 16px;
  }

  .rotate-icon {
    transform: rotate(100deg);
  }

  .button-add {
    height: 19px;
    width: 109px;
    color: #FFFFFF;
  }

</style>

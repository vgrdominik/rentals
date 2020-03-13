<template>
  <div>
    <!-- Initial -->
    <v-container
      class="fill-height mb-12 pt-12 pb-12"
      fluid style="background-color: #BCE0FD;">
      <v-row dense style="z-index: 1;">
        <v-col cols="12">
          <vue-particles
            color="#54B5EE"
            :particleOpacity="0.7"
            :particlesNumber="80"
            shapeType="circle"
            :particleSize="4"
            linesColor="#424242"
            :linesWidth="1"
            :lineLinked="true"
            :lineOpacity="0.4"
            :linesDistance="150"
            :moveSpeed="3"
            :hoverEffect="true"
            hoverMode="grab"
            :clickEffect="true"
            clickMode="push" />
        </v-col>
      </v-row>
      <v-row dense align="center" justify="center" style="position: absolute; height: 100%; width: 100%; z-index: 2;">
        <v-spacer />
        <v-col cols="12" sm="5" class="text-center">
          <h1 class="primary--text display-2 font-weight-black">Haz dinero alquilando tus cosas.</h1>
          <v-row dense class="mt-4">
            <v-spacer />
            <v-col cols="4">
              <img src="~/assets/apple-store-btn.png" style="width: 100%;" />
            </v-col>
            <v-col cols="4">
              <img src="~/assets/google-store-btn.png" style="width: 100%;" />
            </v-col>
            <v-spacer />
          </v-row>
        </v-col>
        <v-spacer />
        <v-col cols="6" v-if="$vuetify.breakpoint.smAndUp" class="text-center">
          <img src="~/assets/mobil.png" style="width: auto; max-height:650px" />
        </v-col>
      </v-row>
    </v-container>

    <!-- How it works -->
    <v-container class="mt-12 mb-12 pt-12 pb-12">
      <v-row dense align="center" justify="center">
        <v-spacer />
        <v-col cols="8" class="text-center">
          <v-row dense>
            <v-col cols="12">
              <h1 class="secondary--text display-2 font-weight-black">¿Cómo funciona?</h1>
            </v-col>
            <v-col cols="12" class="secondary--text headline">
              ¿Tienes algo que quieres compartir con el mundo?<br>
              Alquilarlo es fácil, flexible, seguro y rápido.<br>
              ¿Tienes cosas de valor que puedas alquilar?
            </v-col>
          </v-row>
        </v-col>
        <v-spacer />
      </v-row>
      <v-row dense class="mt-12">
        <v-col cols="12" md="3">
          <div class="text-center">
            <CtIcon :icon="['fa', 'th-list']" class="primary--text display-4" />
          </div>
          <h1 class="text-center secondary--text display-1 font-weight-black mt-3">Busca</h1>
          <div class="text-center secondary--text headline">
            Busca entre todos los artículos para alquilar.
          </div>
        </v-col>
        <v-col cols="12" md="3">
          <div class="text-center">
            <CtIcon :icon="['fa', 'calendar-alt']" class="primary--text display-4" />
          </div>
          <h1 class="text-center secondary--text display-1 font-weight-black mt-3">Reserva</h1>
          <div class="text-center secondary--text headline">
            Reserva un alquiler durante el tiempo que necesites.
          </div>
        </v-col>
        <v-col cols="12" md="3">
          <div class="text-center">
            <CtIcon :icon="['fa', 'play']" class="primary--text display-4" />
          </div>
          <h1 class="text-center secondary--text display-1 font-weight-black mt-3">Utiliza</h1>
          <div class="text-center secondary--text headline">
            Disfruta tu alquiler como desees.
          </div>
        </v-col>
        <v-col cols="12" md="3">
          <div class="text-center">
            <CtIcon :icon="['fa', 'undo-alt']" class="primary--text display-4" />
          </div>
          <h1 class="text-center secondary--text display-1 font-weight-black mt-3">Devuélve</h1>
          <div class="text-center secondary--text headline">
            Retorna el material en las condiciones originales.
          </div>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import { mapActions } from 'vuex'

export default {

  mounted() {
    this.setIsContainerNeeded(false)
  },

  methods: {
    ...mapActions({
      setIsContainerNeeded: 'global/setIsContainerNeeded',
    }),
  },
}
</script>

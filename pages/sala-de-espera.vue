<template>
    <CtCard title="Sala de espera" width="300" class="mx-auto">
      <v-row dense>
        <v-col cols="12" class="mt-5">
          En breves momentos serás redirigido hacia la página de emprendimiento.
        </v-col>
        <v-col cols="12" class="mt-5">
          <v-row>
            <v-spacer />
            <v-subheader v-html="'¿Ha pasado más de 5 segundos?'" />
            <v-spacer />
          </v-row>
        </v-col>
        <v-col cols="12" class="my-5">
          <CtBtn to="/emprendimiento" type="accent" block>
            Ir a emprendimiento
          </CtBtn>
        </v-col>
      </v-row>
    </CtCard>
</template>

<script>
import { mapActions } from 'vuex'
export default {
  mounted() {
    this.setIsContainerNeeded(true)
    setTimeout(() => this.$router.push({ path: '/emprendimiento' }), 3000)
  },

  methods: {

    ...mapActions({
      setIsContainerNeeded: 'global/setIsContainerNeeded',
      setServerMessage: 'serverMessage/setServerMessage',
    }),
  }
}
</script>

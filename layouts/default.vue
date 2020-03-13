<template>
  <v-app id="inspire">
    <v-navigation-drawer
      v-model="drawer"
      :clipped="$vuetify.breakpoint.lgAndUp"
      app
    >
      <v-list dense>
        <template v-for="item in items">
          <v-row
            v-if="item.heading"
            :key="item.heading"
            align="center"
          >
            <v-col cols="12">
              <v-subheader v-if="item.heading">
                {{ item.heading }}
              </v-subheader>
            </v-col>
          </v-row>
          <v-list-group
            v-else-if="item.children"
            :key="item.text"
            v-model="item.model"
            append-icon=""
          >
            <template v-slot:activator>
              <v-list-item-content @click="$router.push({ path: item.path })">
                <v-list-item-title class="primary--text">
                  {{ item.text }}
                </v-list-item-title>
              </v-list-item-content>
            </template>
            <v-list-item
              v-for="(child, i) in item.children"
              :key="i"
              link
            >
              <v-list-item-action v-if="child.icon" @click="$router.push({ path: child.path })">
                <CtIcon :icon="child.icon" class="primary--text" />
              </v-list-item-action>
              <v-list-item-content @click="$router.push({ path: child.path })">
                <v-list-item-title class="primary--text">
                  {{ child.text }}
                </v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list-group>
          <v-list-item
            v-else
            :key="item.text"
            link
          >
            <v-list-item-action @click="$router.push({ path: item.path })">
              <CtIcon :icon="item.icon" class="primary--text" />
            </v-list-item-action>
            <v-list-item-content @click="$router.push({ path: item.path })">
              <v-list-item-title class="primary--text">
                {{ item.text }}
              </v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </template>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      :clipped-left="$vuetify.breakpoint.lgAndUp"
      app
      dark
      color="primary"
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title
        style="width: 300px"
        class="ml-0 pl-4"
      >
        <CtBtn type="text" color="white" to="/">Rentals</CtBtn>
      </v-toolbar-title>
      <v-spacer />

      <template v-if="user">
        <CtBtn type="text" color="white" @click="logout()">
          Salir
        </CtBtn>
      </template>
      <template v-else>
        <CtBtn type="text" color="white" to="/login">
          Login
        </CtBtn>
        |
        <CtBtn type="text" color="white" to="/registro">
          Registro
        </CtBtn>
      </template>
      <template v-if="user">
        <CtBtn type="icon" :icon="['fas', 'bell']" to="/notificaciones" />
      </template>
    </v-app-bar>
    <v-content>
      <nuxt v-if="! isContainerNeeded" />
      <v-container
        class="fill-height"
        fluid
        v-else
      >
        <nuxt />
      </v-container>
    </v-content>

    <v-footer padless>
      <CtCard type="empty" flat tile width="100%" class="primary white--text text-center">
        <v-card-text>
          <CtBtn v-for="footerItem in footerItems" :key="footerItem.title" type="icon" target="_blank" :title="footerItem.title" :href="footerItem.href" :icon="footerItem.icon" class="mx-4 white--text" />
        </v-card-text>

        <v-card-text class="white--text pt-0">
          Con rentals puedes hacer dinero alquilando tus cosas.
        </v-card-text>

        <v-divider></v-divider>

        <v-card-text class="white--text">
          <CtBtn type="text" href="https://www.ciclotic.com/sobre-ciclotic.php#condiciones" target="_blank" color="white">Condiciones</CtBtn>
          <CtBtn type="text" href="https://valentigamez.com" target="_blank" color="white">{{ new Date().getFullYear() }} — Rentals</CtBtn>
        </v-card-text>
      </CtCard>
    </v-footer>
  </v-app>
</template>

<script>
import { mapMutations, mapActions } from 'vuex'

export default {
  props: {
    source: String,
  },

  data: () => ({
    dialog: false,
    drawer: false,
    items: [
      { icon: ['fas', 'asterisk'], text: 'Inicio', path: '/' },
      { icon: ['fas', 'asterisk'], text: 'Categoría blog 1', path: '/categoria-1' },
      { icon: ['fas', 'asterisk'], text: 'Categoría blog 2', path: '/categoria-2' },
      { icon: ['fas', 'asterisk'], text: 'Cómo funciona', path: '/como-funciona' },
      { icon: ['fas', 'asterisk'], text: 'Preguntas frequentes', path: '/faq' },
      { icon: ['fas', 'asterisk'], text: 'Blog', path: '/blog' },
      { icon: ['fas', 'asterisk'], text: 'Contacto', path: '/contacto' },
    ],
    footerItems: [
      {
        href: 'https://www.facebook.com/iamvalentigamez',
        icon: ['fab', 'facebook'],
        title: 'Página de Facebook',
      },
      {
        href: 'https://twitter.com/iamvalentigamez',
        icon: ['fab', 'twitter'],
        title: 'Pperfil de Twitter',
      },
      {
        href: 'https://www.instagram.com/iamvalentigamez/',
        icon: ['fab', 'instagram'],
        title: 'Perfil de Instagram',
      },
      {
        href: 'https://www.linkedin.com/in/valent%C3%AD-g%C3%A0mez-rojas-5919b073/',
        icon: ['fab', 'linkedin'],
        title: 'Perfil laboral en Linkedin',
      },
      {
        href: 'https://www.youtube.com/vgrdominik',
        icon: ['fab', 'youtube'],
        title: 'Canal de programación',
      },
    ],
  }),

  computed: {
    isContainerNeeded () {
      return this.$store.state.global.is_container_needed
    },

    user () {
      return this.$store.state.user.user
    },
  },

  methods: {
    afterLogout(){
      this.setToken('')
      this.removeUser()
      setTimeout(() => this.$router.push({ path: '/' }), 2000)
    },

    logout () {
      this.$axios.post('/api/logout')
        .then(() => this.afterLogout())
    },

    ...mapActions({
      setToken: 'user/setToken',
    }),

    ...mapMutations({
      removeUser: 'user/removeUser',
    }),
  },
}
</script>

<template>
  <v-app v-scroll="onScroll">
    <v-app-bar
      :flat="!isScrolled"
      :dark="!isScrolled"
      :color="isScrolled ? 'shades white' : 'shades transparent'"
      fixed
    >
      <v-app-bar-nav-icon
        class="d-md-none"
        large
        @click.stop="drawer = !drawer"
      ></v-app-bar-nav-icon>
      <img src="logo_large.png" height="100%" width="auto" />
      <v-toolbar-items class="d-none d-md-flex">
        <v-btn v-for="route in routes" :key="route.title" text :to="route.url">
          {{ route.title }}
        </v-btn>
      </v-toolbar-items>
      <v-spacer />
      <v-btn icon class="mr-2 d-none d-md-flex">
        <v-icon>mdi-cart</v-icon>
      </v-btn>
      <v-btn rounded outlined class="d-none d-md-flex">
        Se connecter
      </v-btn>
    </v-app-bar>
    <v-navigation-drawer
      disable-resize-watcher
      v-model="drawer"
      width="100%"
      class="nav-drawer"
      app
    >
      <v-btn icon x-large class="ma-2" @click.stop="drawer = !drawer">
        <v-icon>mdi-close</v-icon>
      </v-btn>
      <v-spacer />
      <v-list class="text-center" nav>
        <v-list-item v-for="route in routes" :key="route.title">
          <v-list-item-content>
            <v-btn text nuxt :to="route.url" large>{{ route.title }}</v-btn>
          </v-list-item-content>
        </v-list-item>
        <v-divider />
        <v-list-item>
          <v-list-item-content>
            <v-btn text>Panier</v-btn>
          </v-list-item-content>
        </v-list-item>
        <v-btn rounded outlined>
          <v-icon> fa-sign-in-alt </v-icon>
          Se connecter
        </v-btn>
      </v-list>
      <v-spacer />
    </v-navigation-drawer>
    <nuxt />
    <v-footer>
      <span>&copy; 2019</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      title: 'BEA',
      isScrolled: false,
      drawer: false,
      routes: [
        { title: 'Accueil', url: '/' },
        { title: 'Evènements', url: '/inspire' },
        { title: 'Actualités', url: '' },
        { title: 'Boutique', url: '' },
        { title: 'Cafétaria', url: '' }
      ]
    };
  },
  methods: {
    onScroll() {
      const scroll = window.scrollY;
      if (scroll > 0) {
        this.isScrolled = true;
      } else {
        this.isScrolled = false;
      }
    }
  }
};
</script>

<style>
.v-navigation-drawer__content {
  display: flex;
  flex-direction: column;
}
</style>

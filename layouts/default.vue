<template>
  <v-app v-scroll="onScroll">
    <v-app-bar
      :flat="!isScrolled"
      :dark="!isScrolled"
      :color="isScrolled ? 'shades white' : 'shades transparent'"
      fixed
    >
      <v-app-bar-nav-icon class="d-md-none" large @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      <img src="logo_large.png" height="100%" width="auto" />
      <v-toolbar-items class="d-none d-md-flex">
        <v-btn v-for="route in routes" :key="route.title" text :to="route.url">{{ route.title }}</v-btn>
      </v-toolbar-items>
      <v-spacer />
      <v-btn icon class="mr-2 d-none d-md-flex">
        <v-icon>mdi-cart</v-icon>
      </v-btn>
      <v-btn rounded outlined class="d-none d-md-flex">Se connecter</v-btn>
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
          <v-icon>fa-sign-in-alt</v-icon>Se connecter
        </v-btn>
      </v-list>
      <v-spacer />
    </v-navigation-drawer>
    <nuxt />
    <v-footer dark padless class="blue accent-4 flex-column pb-5">
      <svg
        width="100%"
        viewBox="0 0 1440 224"
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        xml:space="preserve"
        xmlns:serif="http://www.serif.com/"
        style="fill-rule:evenodd;clip-rule:evenodd;stroke-linejoin:round;stroke-miterlimit:2;"
        class="pb-5"
      >
        <path
          d="M0,64l80,26.7c80,26.3 240,80.3 400,101.3c160,21 320,11 480,10.7c160,0.3 320,10.3 400,16l80,5.3l0,-224l-80,0l-1280,0l-80,0l0,64Z"
          style="fill:#fff;fill-rule:nonzero;"
        />
      </svg>
      <!-- <h2 class="headline">Nos Sponsors</h2>
      <div class="d-flex"></div>-->
      <h2 class="headline">Plan du site</h2>
      <!-- <span>&copy; 2019</span> -->
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

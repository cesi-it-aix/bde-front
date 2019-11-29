<template>
  <v-content>
    <waved-header :gradient="headerGradient">
      <slot name="header"></slot>
      <template v-slot:secondary>
        <slot name="header-secondary"></slot>
      </template>
    </waved-header>
    <div class="layout-container">
      <v-container>
        <slot></slot>
      </v-container>
    </div>
  </v-content>
</template>

<script>
import WavedHeader from '~/components/Header/Header.vue';

export default {
  props: {
    headerGradient: Boolean
  },
  components: { WavedHeader }
};
</script>

<style scoped>
.layout-container {
  position: relative;
  z-index: 2;
  background-color: #fff;
}
</style>

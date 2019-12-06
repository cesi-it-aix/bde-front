<template>
  <div class="header" :class="{ diagonal: isDiagonal }">
    <div class="header-background" :class="{ gradient }">
      <div class="d-flex justify-center">
        <slot></slot>
      </div>
      <template v-if="isDiagonal">
        <diagonal-wave class="d-none d-md-block" />
        <default-wave class="d-block d-md-none" />
      </template>
      <default-wave v-else />
    </div>
    <div class="header-wave">
      <div class="d-flex justify-center">
        <template v-if="isDiagonal">
          <slot name="secondary"></slot>
        </template>
        <slot v-else></slot>
      </div>
      <template v-if="isDiagonal">
        <diagonal-wave class="d-none d-md-block" />
        <default-wave class="d-block d-md-none" />
      </template>
      <default-wave v-else />
    </div>
  </div>
</template>

<script>
import DiagonalWave from './DiagonalWave.vue';
import DefaultWave from './HorizontalWave.vue';
export default {
  props: { gradient: Boolean },
  components: { DiagonalWave, DefaultWave },
  computed: {
    isDiagonal() {
      return !!this.$slots['secondary'];
    }
  }
};
</script>

<style scoped>
.header > .header-background {
  position: fixed;
  background: rgb(25, 102, 242);
  color: #fff;
}

.header > .header-background.gradient {
  background: linear-gradient(
    5deg,
    rgba(255, 195, 88, 1) 20%,
    rgba(255, 137, 113, 1) 30%,
    rgba(255, 89, 162, 1) 35%,
    rgba(210, 83, 213, 1) 40%,
    rgba(25, 102, 242, 1) 60%
  );
}

.header > .header-wave {
  position: relative;
}

.header > .header-background > div,
.header > .header-wave > div {
  padding-top: calc(64px + 24px);
  padding-bottom: 24px;
}

.header > .header-background,
.header > .header-wave {
  width: 100%;
}

.header > .header-background > svg,
.header > .header-wave > div {
  visibility: hidden;
}

.header > div > svg {
  max-height: 700px;
}

.header > .header-wave > svg {
  display: block;
  filter: drop-shadow(0px -10px 10px rgba(0, 0, 0, 0.3));
}

@media (min-width: 960px) {
  .header > .header-background.gradient {
    background: linear-gradient(
      20deg,
      rgba(255, 195, 88, 1) 35%,
      rgba(255, 137, 113, 1) 40%,
      rgba(255, 89, 162, 1) 45%,
      rgba(210, 83, 213, 1) 50%,
      rgba(25, 102, 242, 1) 70%
    );
  }
  .header.diagonal > div > div {
    position: absolute;
    height: 100%;
    top: 0;
    flex-direction: column;
    padding-top: 64px;
  }

  .header.diagonal > div > svg {
    padding-top: 64px;
  }

  .header.diagonal > .header-wave > div {
    left: 0;
    z-index: 1;
    visibility: visible;
  }

  .header.diagonal > .header-background > div {
    right: 0;
  }
}
</style>

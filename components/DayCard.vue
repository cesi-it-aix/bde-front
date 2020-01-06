<template>
  <v-card class="day-card px-10 py-5 text-center" tile elevation="10">
    <div>{{month}}</div>
    <div class="display-1 font-weight-black grey--text text--darken-3 my-1">{{day}}</div>
    <div>{{year}}</div>
  </v-card>
</template>

<script>
export default {
  props: {
    date: Date
  },
  computed: {
    month() {
      return new Intl.DateTimeFormat('fr-Fr', { month: 'short' })
        .format(this.date)
        .toUpperCase();
    },
    day() {
      return this.date.getDate();
    },
    year() {
      return this.date.getFullYear();
    }
  }
};
</script>

<style>
.day-card {
  border-radius: 1rem;
}
</style>
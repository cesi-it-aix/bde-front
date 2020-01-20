<template>
  <v-card class="event-card w ma-5" :to="uri" nuxt flat>
    <div class="d-flex" :class="{'flex-row-reverse': rtl}">
      <day-card :date="event.dateStart" />
      <v-list-item two-line :class="{'text-right': rtl}">
        <v-list-item-content>
          <v-list-item-title class="headline mb-1">{{event.title}}</v-list-item-title>
          <v-list-item-subtitle>{{event.summary}}</v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
    </div>
  </v-card>
</template>

<script>
import DayCard from '~/components/DayCard.vue';

export default {
  components: {
    DayCard
  },
  props: {
    event: Object,
    rtl: Boolean
  },
  computed: {
    uri() {
      return `/events/${this.event.id}`;
    }
  }
};
</script>

<style>
.event-card {
  width: 100%;
}
</style>
<template>
  <layout>
    <template v-slot:header>
      <h1>Evènements</h1>
    </template>
    <v-layout>
      <v-flex>
        <section v-for="eventSection in eventSections" v-bind:key="eventSection.title">
          <h3 class="text-center">{{eventSection.title}}</h3>
          <event-card v-for="event in eventSection.events" :event="event" v-bind:key="event.id" />
        </section>
      </v-flex>
    </v-layout>
  </layout>
</template>

<script>
import Layout from '~/components/Layout.vue';
import EventCard from '~/components/EventCard.vue';
import gql from 'graphql-tag';
import { isSameWeek, isSameMonth } from 'date-fns';

export default {
  components: {
    Layout,
    EventCard
  },
  apollo: {
    events: {
      query: gql`
        {
          events(sort: "dateStart:ASC") {
            title
            id
            summary
            content
            dateStart
            dateEnd
          }
        }
      `,
      update(data) {
        return data.events.map(x => ({
          ...x,
          dateStart: new Date(x.dateStart),
          dateEnd: new Date(x.dateEnd)
        }));
      }
    }
  },
  data() {
    return { events: [] };
  },
  computed: {
    eventSections() {
      const now = new Date();
      const weekEvents = [];
      const monthEvents = [];
      const laterEvents = [];
      for (const event of this.events) {
        if (isSameWeek(now, event.dateStart, { weekStartsOn: 1 })) {
          weekEvents.push(event);
        } else if (isSameMonth) {
          monthEvents.push(event);
        } else {
          laterEvents.push(event);
        }
      }
      return [
        {
          title: 'Cette semaine',
          events: weekEvents
        },
        {
          title: 'Ce mois-ci',
          events: monthEvents
        },
        {
          title: 'Plus tard',
          events: laterEvents
        }
      ].filter(x => x.events.length > 0);
    }
  }
};
</script>

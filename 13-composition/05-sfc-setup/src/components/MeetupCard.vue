<template>
  <UiCard tag="article" :cover="meetup.image" class="meetup-card">
    <template #header>
      {{ meetup.title }}
    </template>

    <template #default>
      <UiBadge v-if="meetup.organizing" type="success" class="meetup-card__badge">Организую</UiBadge>
      <UiBadge v-if="meetup.attending" type="primary" class="meetup-card__badge">Участвую</UiBadge>
      <ul class="meetup-info">
        <li class="meetup-info__item">
          <UiIcon icon="user" class="meetup-info__icon" />
          {{ meetup.organizer }}
        </li>
        <li class="meetup-info__item">
          <UiIcon icon="map" class="meetup-info__icon" />
          {{ meetup.place }}
        </li>
        <li class="meetup-info__item">
          <UiIcon icon="cal-lg" class="meetup-info__icon" />
          <time :datetime="isoDate">{{ localDate }}</time>
        </li>
      </ul>
    </template>
  </UiCard>
</template>

<script setup>
import { computed } from 'vue';
import UiBadge from './UiBadge.vue';
import UiCard from './UiCard.vue';
import UiIcon from './UiIcon.vue';

const props = defineProps({
  props: {
    meetup: {
      type: Object,
      required: true,
    },
  },
});

const isoDate = computed(() => new Date(props.meetup.date).toISOString().split('T')[0]);

const localDate = computed(() =>
  new Date(props.meetup.date).toLocaleString(navigator.language, {
    year: 'numeric',
    month: 'long',
    day: 'numeric',
  }),
);
</script>

<style scoped>
.meetup-card {
  position: relative;
}

.meetup-card__badge {
  position: absolute;
  top: 0;
  right: 0;
}

/* meetup-info */
.meetup-info {
  margin: 0;
  padding: 0;
}

.meetup-info__item {
  list-style-type: none;
  position: relative;
  padding-left: 36px;
  font-size: 18px;
  line-height: 28px;
  margin: 0 0 8px;
}

.meetup-info__item:last-child {
  margin: 0;
}

.meetup-info__icon {
  position: absolute;
  left: 0;
  top: 0;
}
</style>

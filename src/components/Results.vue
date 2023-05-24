<template>
  <h2>気象データ</h2>
  <div v-if="results.country">{{ country }}</div>
  <div v-if="results.cityName">{{ cityName }}</div>
  <div v-if="results.temperature">{{ temperature }}</div>
  <div v-if="results.icon">
    <img :src="icon" alt="icon" />
    <span>{{ conditionText }}</span>
  </div>
</template>
<script setup>
import { toRefs } from 'vue';

const props = defineProps({
  results: Object,
});
const { country, cityName, temperature, icon, conditionText } = toRefs(
  props.results
);
</script>

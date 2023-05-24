<template>
  <div class="wrapper">
    <div class="container">
      <Title />
      <Form @submit-form="getWeather" />
      <Results :results="results" />
    </div>
  </div>
</template>

<script setup>
import { reactive } from 'vue';
import axios from 'axios';
import Title from './components/Title.vue';
import Form from './components/Form.vue';
import Results from './components/Results.vue';
import './assets/base.css';
const getWeather = (city) => {
  axios
    .get(
      `http://api.weatherapi.com/v1/current.json?key=05051e5cbe434679aab04822232405&q=${city}&aqi=no`
    )
    .then((res) => {
      (results.country = res.data.location.country),
        (results.cityName = res.data.location.name),
        (results.temperature = res.data.current.temp_c),
        (results.conditionText = res.data.current.condition.text),
        (results.icon = res.data.current.condition.icon);
    });
};
const results = reactive({
  country: '',
  cityName: '',
  temperature: '',
  conditionText: '',
  icon: '',
});
</script>

<template>
  <div class="wrapper">
    <div class="container">
      <Title />
      <Form @submit-form="getWeather" />
      <Results :results="results" v-if="!loading" />
      <loading v-if="loading" />
    </div>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue';
import axios from 'axios';
import Title from './components/Title.vue';
import Form from './components/Form.vue';
import Results from './components/Results.vue';
import './assets/base.css';
import Loading from './components/Loading.vue';
const loading = ref(false);
const getWeather = (city) => {
  loading.value = true;
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
      loading.value = false;
    })
    .catch((err) => alert('error try plz'));
};
const results = reactive({
  country: '',
  cityName: '',
  temperature: '',
  conditionText: '',
  icon: '',
});
</script>

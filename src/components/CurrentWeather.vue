<template>
  <div class="row weather-card border-bottom" v-if="weather">
    <div class="col-md-6 mx-auto text-center">
      <h3>{{weather.city}}</h3>
      <span class="temp" style="font-size: 4rem">{{ weather.temperature + "°" }}</span>
      <p>{{ weather.summary }}</p>
    </div>
  </div>
</template>

<script>
import { reactive } from "vue";

export default {
  name: "CurrentWeather",
  props: {
    weather: Object,
  },
  setup() {
    const state = reactive({
      iconLink: "https://darksky.net/images/weather-icons/",
    });

    return { state };
  },
};
</script>

<style lang="css" scoped>

</style>

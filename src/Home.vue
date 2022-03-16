<template>
  <div class="container">
    <search @search-result="getWeather" />
    <current-weather :weather="state.weather" />
    <coming-days :data="state.data" />
  </div>
</template>

<script>
import search from "@/components/Search.vue";
import { reactive } from "vue";
import CurrentWeather from "./components/CurrentWeather.vue";
import ComingDays from "./components/ComingDays.vue";

export default {
  name: "Home",
  components: {
    search,
    CurrentWeather,
    ComingDays,
  },

  setup() {
    const state = reactive({
      weather: null,
      data: null,
      key: "1d5cfbb4b1ba74f6287033207b5f59d7",
    });

    async function getWeather(city) {
      
      const proxy = "https://cors-anywhere.herokuapp.com/";
      const apiUrl = `https://api.darksky.net/forecast/${state.key}/${city.latlng.lat},${city.latlng.lng}?lang=en&units=ca`;
      const data = await fetch(proxy + apiUrl);
      const resData = await data.json();

    console.log(resData);
      const currentWeather = {
        city : city.name,
        summary: resData.currently.summary,
        temperature: Math.round(resData.currently.temperature),
      };
      state.weather = currentWeather;

      state.data = resData.daily.data.splice(1,8);
    }
    return { getWeather, state };
  },
};
</script>

<style lang="css" scoped></style>

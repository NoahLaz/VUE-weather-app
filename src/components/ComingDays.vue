<template>
  <div class="row weather-card border-bottom" v-if="data">
    <div
      class="col-md-3 mx-auto text-center"
      v-for="(day, index) in data"
      :key="index"
    >
      <h3>{{ convertTimestamp(day.time) }}</h3>
      <img
        :src="state.iconLink + day.icon + '.png'"
        width="50"
        height="50"
        alt="weather icon"
      />
      <p style="font-size: 2rem">
        <span>{{ Math.round(day.temperatureHigh) + "°C" }}</span>
        -
        <span>{{ Math.round(day.temperatureLow) + "°C" }}</span>
      </p>
      <p>{{ day.summary }}</p>
    </div>
  </div>
</template>

<script>
import { reactive } from "vue";
import moment from "moment";
import "moment/locale/en-gb";

export default {
  name: "ComingDays",
  props: {
    data: Object,
  },
  setup() {
    const state = reactive({
      iconLink: "https://darksky.net/images/weather-icons/",
    });
    function convertTimestamp(time) {
      let day = moment.unix(time).locale("en").utc();
      return day.format("dddd MM Do");
    }

    return { state, convertTimestamp };
  },
};
</script>

<style lang="css" scoped></style>

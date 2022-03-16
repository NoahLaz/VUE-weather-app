<template>
  <div class="row my-4">
    <div class="col-md-6 mx-auto">
      <div class="form-group">
        <input
          type="search"
          autocomplete="off"
          class="form-control"
          id="adress-input"
          placeholder="Enter city"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { onMounted, reactive } from "vue";
import places from "places.js";

export default {
  name: "Search",
  emits: ["search-result"],

  setup(props, { emit }) {
    const state = reactive({
      appId: "pl84BDTK7HU7",
      apiKey: "671cd803cf905b98ff3217c773e5207a",
    });

    function getPlaces() {
      let placesAutoComplete = places({
        appId: state.appId,
        apiKey: state.apiKey,
        container: document.querySelector("#adress-input"),
      });
      placesAutoComplete.on("change", function ($e) {
        emit("search-result", $e.suggestion);
      });
    }

    onMounted(() => {
      getPlaces();
    });

    return {};
  },
};
</script>

<style lang="css" scoped></style>

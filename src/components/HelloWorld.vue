<template>
  <v-row justify="center">
    <v-col cols="4" class="mt-10 pt-10">
      <v-row>
        <v-col cols="12" class="text-center text-h5 text-uppercase"
          >Write a Location</v-col
        >
        <v-col cols="12">
          <v-text-field
            variant="outlined"
            title="Location"
            class="text-blue"
            placeholder="London"
            v-model="getWeatherValueName"
            @keyup.enter="searchLocation"
          ></v-text-field>
        </v-col>
        <v-col cols="12" class="text-center">
          <v-btn width="100%" height="70" title="search">
            <v-row>
              <v-col
                class="text-overlined font-weight-medium text-blue-darken-4"
                style="letter-spacing: 4px"
                @click="searchLocation"
                >SEARCH</v-col
              >
            </v-row>
          </v-btn>
        </v-col>
      </v-row>
    </v-col>
  </v-row>
  <v-row v-show="getWeatherData !== ''">
    <v-col cols="12" >
      <v-container>
        <v-row justify="center">
          <v-col cols="8">
            <v-card height="500" class="pa-5">
              <v-row class="text-center">
                <v-col
                  cols="12"
                  class="text-overlined text-uppercase"
                  style="letter-spacing: 15px"
                  >{{ getWeatherData.location.name }}</v-col
                >
                <v-col
                  cols="3"
                  class="text-overlined font-weight-black text-end"
                  >Country:</v-col
                >
                <v-col cols="3" class="text-start">B</v-col>
                <v-col
                  cols="3"
                  class="text-overlined font-weight-black text-end"
                  >Region:</v-col
                >
                <v-col cols="3" class="text-start">C</v-col>
                <v-col
                  cols="6"
                  class="text-overlined font-weight-black text-end"
                  >Local Time:</v-col
                >
                <v-col cols="6" class="text-start">D</v-col>
                <v-col
                  cols="3"
                  class="text-overlined font-weight-black text-end"
                  >Region:</v-col
                >
                <v-col cols="3" class="text-start">E</v-col>
                <v-col
                  cols="3"
                  class="text-overlined font-weight-black text-end"
                  >Cloud:</v-col
                >
                <v-col cols="3" class="text-start">%E</v-col>
              </v-row>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-col>
    <v-col cols="8"></v-col>
  </v-row>
</template>

<script lang="ts">
import axios from "axios";
export default {
  data() {
    return {
      getWeatherValueName: "London" as any,
      getWeatherData: [] as any,
    };
  },
  methods: {
    searchLocation() {
      axios
        .get(
          "http://api.weatherapi.com/v1/current.json?key=35e9395db92d4a2e80263200230902&q=" +
            this.getWeatherValueName +
            "&aqi=yes"
        )
        .then((res: any) => (this.getWeatherData = res.data))
        .catch((e: any) => console.log("error"));
    },
  },
  watch: {
    getWeatherData: {
      handler(newValue, oldValue) {
        console.log(newValue);
      },
      deep: true,
    },
  },
};
</script>

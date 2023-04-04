<template>
  <v-app>
    <v-img
      src="https://cdn.pixabay.com/photo/2016/03/27/07/32/clouds-1282314__480.jpg"
      cover
    >
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
              <v-btn
                width="100%"
                height="70"
                title="search"
                class="btnOpac"
                rounded
              >
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
      <v-row v-if="getShowLocation">
        <v-col cols="12">
          <v-container >
            <v-row justify="center">
              <v-col cols="8">
                <v-card height="100%" class="pa-5 btnOpac">
                  <v-row justify="center">
                    <v-col cols="4">
                      <v-img :src="getImage" width="100%"></v-img>
                    </v-col>
                  </v-row>
                  <v-row class="text-center">
                    <v-col
                      cols="12"
                      class=" text-uppercase text-purple-darken-4"
                      style="letter-spacing: 20px"
                      >{{ getName }}</v-col
                    >
                    <v-col
                      cols="6"
                      sm="6"
                      md="3"
                      lg="3"
                      xl="3"
                      class="text-overline font-weight-black text-end text-red"
                      >Country:</v-col
                    >
                    <v-col
                      cols="6"
                      sm="6"
                      md="3"
                      lg="3"
                      xl="3"
                      class="text-start text-overline text-indigo-darken-4"
                      >{{ getCountry }}</v-col
                    >

                    <v-col
                      cols="6"
                      sm="6"
                      md="3"
                      lg="3"
                      xl="3"
                      class="text-overline font-weight-black text-end text-red"
                      >Local Time:</v-col
                    >
                    <v-col
                      cols="6"
                      sm="6"
                      md="3"
                      lg="3"
                      xl="3"
                      class="text-start text-overline text-indigo-darken-4"
                      >{{ getLocalTime }}</v-col
                    >
                    <v-col
                      cols="6"
                      sm="6"
                      md="3"
                      lg="3"
                      xl="3"
                      class="text-overline font-weight-black text-end text-red"
                      >Region:</v-col
                    >
                    <v-col
                      cols="6"
                      sm="6"
                      md="3"
                      lg="3"
                      xl="3"
                      class="text-start text-overline text-indigo-darken-4"
                      >{{ getRegion }}</v-col
                    >
                    <v-col
                      cols="6"
                      sm="6"
                      md="3"
                      lg="3"
                      xl="3"
                      class="text-overline font-weight-black text-end text-red"
                      >Cloud:</v-col
                    >
                    <v-col
                      cols="6"
                      sm="6"
                      md="3"
                      lg="3"
                      xl="3"
                      class="text-start text-overline text-indigo-darken-4"
                      >%{{ getCloud }}</v-col
                    >
                  </v-row>
                </v-card>
              </v-col>
            </v-row>
          </v-container>
        </v-col>
      </v-row>
    </v-img>
  </v-app>
</template>

<script lang="ts">
import axios from "axios";
export default {
  data() {
    return {
      getWeatherValueName: "London" as any,
      getWeatherData: {} as any,
      getName: "" as any,
      getCountry: "" as any,
      getRegion: "" as any,
      getLocalTime: "" as any,
      getCloud: "" as any,
      getImage: "" as any,
      getShowLocation: false as any,
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
        .then((res: any) => {
          if (res.status == 200) {
            console.log(res.data);
            this.getName = res.data.location.name;
            this.getCountry = res.data.location.country;
            this.getRegion = res.data.location.region;
            this.getLocalTime = res.data.location.localtime;
            this.getImage = res.data.current.condition.icon;
            this.getCloud = res.data.current.cloud;
            this.getShowLocation = true;
          }
        })
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
<style scoped>
.btnOpac {
  background-color: rgba(255, 255, 255, 0.708);
}
</style>

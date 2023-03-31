<template>
    <div v-if="!weatherReport.error" >
        <div class="bg-cyan-700 flex flex-col h-full gap-24 p-10 pb-8">
          <div class="text-center text-white flex justify-between items-center  bg-cyan-600 rounded-md p-4">
            <div class="flex flex-col gap-3">
              <h1 class="opacity-50">COUNTRY</h1>
              <h1 class="text-4xl">{{ weatherReport?.location?.country }}</h1>
            </div>
            <div class="flex flex-col gap-3">
              <h1 class="opacity-50">REGION</h1>
              <h1 class="text-4xl">{{ weatherReport?.location?.region }}</h1>
            </div>
            <div class="flex flex-col gap-3">
              <h1 class="opacity-50">PLACE</h1>
              <h1 class="text-4xl">{{ weatherReport?.location?.name }}</h1>
            </div>
            <div class="flex flex-col gap-3">
              <h1 class="opacity-50">LOCAL DATE AND TIME</h1>
              <h1 class="text-4xl">{{ weatherReport?.location?.localtime }}</h1>
            </div>
          </div>
      
          <div
            class="text-center text-white flex justify-between items-center  bg-cyan-600 rounded-md p-4"
          >
            <div>
              <h1 class="opacity-50">Weather condition</h1>
              <h1 class="text-4xl">{{ weatherReport?.current?.condition?.text }}</h1>
            </div>
            <img
              class="w-28 h-28 pt-3"
              :src="weatherReport?.current?.condition?.icon"
            />
            <img
              class="w-28 h-28 pt-3"
              :src="weatherReport?.current?.condition?.icon"
            />
            <div class="flex flex-col gap-3">
              <h1 class="opacity-50">CLOUD</h1>
              <h1 class="text-4xl">{{ weatherReport?.current?.cloud }}</h1>
            </div>
          </div>
          <div class="text-white  bg-cyan-600 p-4 rounded-md  flex flex-col">
            <h1 class="text-4xl text-center font-sans font-bold shadow-xl mb-3 pb-4">
              Temperature
            </h1>
            <div class="text-center text-white flex gap-3 justify-between px-8 mt-5">
              <div class="flex flex-col gap-3">
                <h1 class="text-2xl opacity-70">In celcius</h1>
                <h1 class="text-4xl">{{ weatherReport?.current?.temp_c }} °C</h1>
              </div>
              <div class="flex flex-col gap-3">
                <h1 class="text-2xl opacity-70">In Fahrenheit</h1>
                <h1 class="text-4xl">{{ weatherReport?.current?.temp_f }} °F</h1>
              </div>
              <div class="flex flex-col gap-3">
                <h1 class="text-2xl opacity-70">Feels Like</h1>
                <h1 class="text-4xl">{{ weatherReport?.current?.feelslike_c }} °C</h1>
              </div>
            </div>
          </div>
          <div class="text-white  bg-cyan-600 flex flex-col p-4 rounded-md">
            <h1 class="text-4xl text-center font-sans font-bold shadow-xl mb-3 pb-4">
              Wind Condition
            </h1>
            <div class="text-center text-white flex gap-3 justify-between px-8 mt-5">
              <div class="flex flex-col gap-3">
                <h1 class="text-2xl opacity-70">Wind Degree</h1>
                <h1 class="text-4xl">{{ weatherReport?.current?.wind_degree }}</h1>
              </div>
              <div class="flex flex-col gap-3">
                <h1 class="text-2xl opacity-70">Wind Direction</h1>
                <h1 class="text-4xl">{{ weatherReport?.current?.wind_dir }}</h1>
              </div>
              <div class="flex flex-col gap-3">
                <h1 class="text-2xl opacity-70">Wind Speed</h1>
                <h1 class="text-4xl">{{ weatherReport?.current?.wind_kph }} Km/hr</h1>
              </div>
              <div class="flex flex-col gap-3">
                <h1 class="text-2xl opacity-70">Wind Speed(m/h)</h1>
                <h1 class="text-4xl">{{ weatherReport?.current?.wind_mph }} M/hr</h1>
              </div>
            </div>
          </div>
      </div>
      <Footer/>
    </div>
    <div v-else class=" flex text-center h-screen bg-cyan-700 justify-center items-center text-white text-4xl ">
        <h1>
            {{weatherReport?.error?.message}} . . . . . . .
        </h1>
    </div>
</template>

<script setup>
import { useRoute } from "vue-router";
import { onMounted, ref } from "vue";
import Footer from "./Footer.vue";
import axios from "axios";
const route = useRoute();
const weatherReport = ref({});

const handleWeatherReport = async () => {
  const options = {
    method: "GET",
    url: "https://weatherapi-com.p.rapidapi.com/current.json",
    params: { q: route.params.place },
    headers: {
      "X-RapidAPI-Key": "ba10621d2fmsha01052307241828p1f1414jsn36cd0d322a67",
      "X-RapidAPI-Host": "weatherapi-com.p.rapidapi.com",
    },
  };
  try { 
      const report = await axios.request(options);
      weatherReport.value = report.data;
      console.log(weatherReport.value);
  } catch (error) {
    weatherReport.value = error.response.data;
  }
};

onMounted(() => {
  handleWeatherReport();
});
</script>

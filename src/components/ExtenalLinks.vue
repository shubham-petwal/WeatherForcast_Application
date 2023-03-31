<template>
  <div class=" mt-5 p-3">
    <h1 class=" mb-5 font-extralight border-b-2 pb-2">AROUND THE GLOBE</h1>
    <div>
      <ul>
        <li v-for="(item, index) in links" :key="index" class=" border-b-2 mt-3 h-10 flex justify-between">
          <a :href="item.link">{{ item.name }}</a>
          <i class="fa-solid fa-right-long"></i>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
const links = [
  {
    name: "HURRICANE",
    link: "https://www.accuweather.com/en/hurricane",
  },
  {
    name: "SEVERE WEATHER",
    link: "https://www.accuweather.com/en/in/severe-weather",
  },
  {
    name: "RADAR & MAPS",
    link: "https://www.accuweather.com/en/in/andhra-pradesh/weather-radar",
  },
  {
    name: "NEWS",
    link: "https://www.accuweather.com/en/weather-news",
  },
  {
    name: "VIDEO",
    link: "https://www.accuweather.com/en/videos",
  },
  {
    name: "PODCASTS",
    link: "https://www.accuweather.com/podcast",
  },
];
</script>

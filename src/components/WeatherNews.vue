<template>
  <div></div>
</template>

<script setup>
import axios from "axios";
import { onMounted } from "vue";

const getNews = async () => {
  const options = {
    method: "GET",
    url: "https://weatherapi-com.p.rapidapi.com/current.json",
    params: { q: "india" },
    headers: {
      "X-RapidAPI-Key": "ba10621d2fmsha01052307241828p1f1414jsn36cd0d322a67",
      "X-RapidAPI-Host": "weatherapi-com.p.rapidapi.com",
    },
  };

  const news = await axios.request(options);
};

onMounted(()=>{
    getNews();
})
</script>

<template>
  <header
    class="h-1/2 flex shadow-lg text-white"
    :style="{
      backgroundSize: 'cover',
      backgroundImage: 'url(' + currentValue + ')',
    }"
  >
    <nav class="container flex flex-col gap-4 py-6 w-3/4">
      <div class="flex">
        <div class="flex flex-1 gap-5">
          <i class="fa-solid fa-sun text-5xl text-yellow-300"></i>
          <h1 class="text-4xl">AccuWeather</h1>
          <h1 class="text-4xl"></h1>
        </div>
        <div class="">
          <i class="fa-solid fa-bars hover:cursor-pointer" @click="emits('showSidebar',true)"></i>
        </div>
      </div>

      <div class="mt-12 flex flex-col gap-6">
        <div
          class="w-4/6 h-14 flex items-center rounded-md bg-white p-3 text-black gap-2 relative"
        >
          <i class="fa-solid fa-search text-2xl"></i>
          <input
            type="text"
            @input="getCountry"
            v-model="searchQuery"
            class="w-4/5 h-14 p-1 text-2xl focus:outline-none"
            placeholder="Search "
          />
          <button class="  hover:opacity-60" @click="showWeather">Search</button>
          <i class="fa fa-chevron-down" aria-hidden="true"></i>
        </div>
        <div v-if="isSearch" class=" absolute bg-white text-black w-3/6 z-50 top-52 max-h-60 overflow-scroll">
          <ul>
            <li v-for="(item, index) in searchedCountries" :key="index" @click="selectCountry(item.name.common)" class=" hover:cursor-pointer text-2xl  h-14 flex items-center pl-3 hover:bg-slate-200">
              {{ item.name.common }}
            </li>
          </ul>
        </div>
        <div>
          <h1 class=" ">RECENT LOCATIONS</h1>
          <div class="backdrop-blur-xl w-56 mt-4 rounded-lg p-4 border">
            <span>Bangalore</span>
            <p>India</p>
            <div class="flex mt-4">
              <i class="fa-solid fa-sun text-5xl"></i>
              <span>30°</span>
              <p>C</p>
            </div>
            <span> RealFeet 30° </span>
          </div>
        </div>
      </div>
    </nav>
  </header>
</template>

<script setup>
import axios from 'axios'
import { ref, onMounted } from "vue";
import { useRouter } from 'vue-router';
const emits = defineEmits(['showSidebar'])
const searchQuery = ref("")
const isSearch = ref(false)
const searchedCountries = ref("")
const weatherImages = ["https://www.awxcdn.com/adc-assets/images/hero/2/1920x450.jpg","https://www.awxcdn.com/adc-assets/images/hero/5/1920x450.jpg",
  "https://images.unsplash.com/photo-1609645778471-613f21fcf3df?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxzZWFyY2h8Mnx8dmVydGljYWwlMjB3YWxscGFwZXJ8ZW58MHx8MHx8&w=1000&q=80",
  "https://images.unsplash.com/photo-1502472584811-0a2f2feb8968?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxleHBsb3JlLWZlZWR8NHx8fGVufDB8fHx8&w=1000&q=80",
  "https://images.unsplash.com/photo-1612527846486-ee50d5702d09?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxzZWFyY2h8NHx8cmVkJTIwY2xvdWR8ZW58MHx8MHx8&w=1000&q=80",
];


const router = useRouter();
const currentIndex = ref(0);
const currentValue = ref(weatherImages[0]);
const updateValue = () => {
  setInterval(() => {
    currentIndex.value = (currentIndex.value + 1) % weatherImages.length;
    currentValue.value = weatherImages[currentIndex.value];
  }, 15000);
};
const getCountry =async() =>{
  isSearch.value = true
  const detail = await axios.get("https://restcountries.com/v3.1/all")
  const countries = await detail.data.filter((item)=>{
    if(item.name.common.includes(searchQuery.value)){
      return item.name.common
    }
  }
  )
  searchedCountries.value = countries
  if(searchQuery.value.length==0){
    isSearch.value = false
  }
  }
  const selectCountry = (name)=>{
    searchQuery.value = name
    isSearch.value = false
    showWeather()
  }
  const showWeather = ()=>{
    if(searchQuery.value){
      router.push({
        name:"weatherView",
        params: {place: searchQuery.value}
      })
    }
  }
  onMounted(() => {
    updateValue();
  });
</script>

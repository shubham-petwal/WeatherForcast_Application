<template>
  <div class="flex flex-col min-h-screen bg-gray-100">
    <Transition>
      <SidebarRight v-if="isSidebar" @close-sidebar="updateSidebar"/>
    </Transition>
    <SiteNavigation @show-sidebar="updateSidebar"/>
    <TopStories/>
    <RouterView />
    <WeatherNews/>
    <Footer/>
  </div>
</template>

<script setup>
import {ref} from "vue";
import { RouterView } from "vue-router";
import WeatherNews from "../components/WeatherNews.vue";
import SidebarRight from "../components/SidebarRight.vue";
import SiteNavigation from "../components/SiteNavigation.vue"
import TopStories from "../components/TopStories.vue";
import Footer from "../components/Footer.vue";
const isSidebar = ref(false)
const updateSidebar = (value)=>{
  isSidebar.value = value
}

</script>

<style>
.v-enter-active {
  transition: all 0.7s ease-out;
}

.v-leave-active {
  transition: all 0.5s cubic-bezier(1, 0.5, 0.8, 1);
}

.v-enter-from,
.v-leave-to {
  transform: translateX(20px);
  opacity: 0;
}
</style>

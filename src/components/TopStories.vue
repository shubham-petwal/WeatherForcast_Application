<template>
    <div class="flex justify-around mt-10">
        <div>
            <Map/>
            <ExtenalLinks/>
        </div>
        <div class=" w-96 border bg-white rounded-md">
            <h1 class="h-16 text-2xl font-bold border-b-2 p-3">Top Stories</h1>
            <div>
                <ul>
                    <li v-for="item in news" :key="item.source_id" class=" flex flex-col gap-2 border-b-2 h-28 p-3 overflow-scroll hover:cursor-pointer">
                        <span class=" text-2xl font-serif mb-1">{{ item.source_id }}</span>
                        <span class="flex">
                            <p class="mr-1">
                                Title:
                            </p>
                            <p class="font-extralight">
                                {{ item.title }}
                            </p>
                        </span>
                        <span class="flex">
                            <p class="mr-1">
                                Content:
                            </p>
                            <p class="font-extralight">
                                {{ item.content }}
                            </p>
                        </span>
                        <span>
                            Pubished At : {{ item.pubDate }}
                        </span>
                        <a :href="item.link" class=" text-blue-700 flex justify-center">
                            Click for more info 
                        </a>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>


<script setup>
import axios from "axios";
import Map from "./Map.vue";
import ExtenalLinks from "./ExtenalLinks.vue";
import { onMounted, ref } from "vue";
const news = ref({})

onMounted(async()=>{
    try {      
        const response = await axios.get("https://newsdata.io/api/1/news?apikey=pub_1960736023f1ebca7cb4ab2d581d6401e1eda&q=pizza")
        news.value = response.data.results
    } catch (error) {
        console.log(error)
    }
})
</script>

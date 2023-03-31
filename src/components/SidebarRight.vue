<template>
    <div>
        <div class="h-screen w-96 p-8 bg-white border-l-2 shadow-md absolute right-0 transition-transform	 duration-1000">
            <div class="flex justify-between items-center text-2xl  h-10">
                <div class="flex gap-2 items-center">
                    <i class="fa-solid fa-gear"></i>
                    <p>Settings</p>
                </div>
                <i class="fa-regular fa-x hover:cursor-pointer" @click="emits('closeSidebar',false)"></i>
            </div>
            <div class=" border-b h-10 mt-3">
                <p>NELLORE, ANDHRA PRADESH WEATHER</p>
            </div>
            <div>
                <ul>
                    <li v-for="(item,index) in sidebarData" :key="index" class=" h-10 gap-2 pt-2 font-mono opacity-60 hover:cursor-pointer">
                        {{item}}
                    </li>
                </ul>
            </div>
            <div class=" mt-7">
                <p class="h-10 border-b-2">AROUND THE GLOBE</p>
                <ul>
                    <li v-for="(item,index) in sidebarData2" :key="index" class=" h-10 gap-2 pt-2 font-mono opacity-60 hover:cursor-pointer">
                        {{item}}
                    </li>
                </ul>
            </div>


        </div>
    </div>
</template>

<script setup>
const emits = defineEmits(['closeSidebar'])
const sidebarData = ["Today","Hourly","Daily","Radar","MinuteCast","Monthly","Air Quality","Health & Services"]
const sidebarData2 = ["Hurricane","Severe Wheather","Radar and Maps","News","Video","Podcasts"]


</script>
<template>
  <div>
    <div class="flex flex-col items-center bg-gray-50 border-b-2">
      <div class="w-screen h-14 border-y flex justify-center">
        <div class="flex h-14 items-center w-4/6 gap-3 opacity-50">
          <p>World</p>
          <i class="fa-solid fa-chevron-right"></i>
          <p>Asia</p>
          <i class="fa-solid fa-chevron-right"></i>
          <p>India</p>
          <i class="fa-solid fa-chevron-right"></i>
          <p>Haryana</p>
          <i class="fa-solid fa-chevron-right"></i>
          <p>Karnal</p>
        </div>
      </div>
      <div class="flex w-4/6 justify-between mt-10 mb-2">
        <div class="">
          <h2 class="opacity-40">COMPANY</h2>
          <ul class="">
            <li
              v-for="(item, index) in footerLinks.company"
              :key="index"
              class="mt-3 mr-3 hover:text-red-400 hover:cursor-pointer"
              style="font-size: 13px"
            >
              <p>{{ item }}</p>
            </li>
          </ul>
          <div class="flex gap-4 mt-4">
            <img
              src="data:image/png;base64,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"
              class="w-8 rounded-full h-8 hover:cursor-pointer hover:opacity-70"
            />
            <img
              class="w-8 rounded-full h-8 hover:cursor-pointer hover:opacity-70"
              src="https://upload.wikimedia.org/wikipedia/en/thumb/0/04/Facebook_f_logo_%282021%29.svg/1200px-Facebook_f_logo_%282021%29.svg.png"
            />
            <img
              class="w-9 rounded-full h-9 hover:cursor-pointer hover:opacity-70"
              src="data:image/jpeg;base64,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"
            />
          </div>
        </div>
        <div class="">
          <h2 class="opacity-40">PRODUCTS & SERVICES</h2>
          <ul class="">
            <li
              v-for="(item, index) in footerLinks.products"
              :key="index"
              class="mt-3 mr-3 hover:text-red-400 hover:cursor-pointer"
              style="font-size: 13px"
            >
              <p>{{ item }}</p>
            </li>
          </ul>
        </div>
        <div>
          <div class="">
            <h2 class="opacity-40">APPS & DOWNLOADS</h2>
            <ul class="">
              <li
                v-for="(item, index) in footerLinks.apps"
                :key="index"
                class="mt-3 mr-3 hover:text-red-400 hover:cursor-pointer"
                style="font-size: 13px"
              >
                <p>{{ item }}</p>
              </li>
            </ul>
          </div>
          <div class="mt-8">
            <h2 class="opacity-40">SUBSCRIPTION SERVICES</h2>
            <ul class="">
              <li
                v-for="(item, index) in footerLinks.subscription"
                :key="index"
                class="mt-3 mr-3 hover:text-red-400 hover:cursor-pointer"
                style="font-size: 13px"
              >
                <p>{{ item }}</p>
              </li>
            </ul>
          </div>
        </div>
        <div class="">
          <h2 class="opacity-40">MORE</h2>
          <ul class="">
            <li
              v-for="(item, index) in footerLinks.more"
              :key="index"
              class="mt-3 mr-3 hover:text-red-400 hover:cursor-pointer"
              style="font-size: 13px"
            >
              <p>{{ item }}</p>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <div class="flex flex-col items-center opacity-50 h-40 justify-center gap-3" style="font-size: 12px">
      <p>
        © 2023 AccuWeather, Inc. "AccuWeather" and sun design are registered
        trademarks of AccuWeather, Inc. All Rights Reserved.
      </p>
      <p class=" font-semibold">Terms of Use | Privacy Policy | Cookie Policy</p>
    </div>
  </div>
</template>

<script setup>
const footerLinks = {
  company: [
    "Proven Superior Accuracy",
    "About AccuWeather",
    "Digital Advertising",
    "Careers",
    "Press",
    "Contact Us",
  ],
  products: [
    "For Business",
    "For Partners",
    "For Advertising",
    "AccuWeather APIs",
    "Podcast",
    "RealFeel® and RealFeel Shade™",
  ],
  apps: ["iPhone App", "Android App", "See all Apps & Downloads"],
  subscription: ["AccuWeather Premium", "AccuWeather Professional"],
  more: [
    "AccuWeather Ready",
    "Business",
    "Health",
    "Hurricane",
    "Leisure and Recreation",
    "Severe Weather",
    "Space and Astronomy",
    "Sports",
    "Travel",
    "Weather News",
  ],
};
</script>

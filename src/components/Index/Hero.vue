<template>
  <div>
    <img class="mx-auto" alt="Image slider slide #1" :src="heroImage" />
    <div
      class="flex flex-col items-start justify-center w-full mx-auto tracking-wide lg:w-1/2"
    >
      <span
        class="w-full p-4 mt-4 text-center text-white bg-black text-md lg:text-2xl lg:-mt-64"
      >
        Modern Interior Sample:From A: {{ store.count }}
      </span>
    </div>
  </div>
</template>

<script setup>
import { store } from '../../lib/store.js'
// https://github.com/ismail9k/vue3-carousel
const heroImage = "/images/Hero.jpg";
</script>

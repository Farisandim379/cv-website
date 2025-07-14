<script setup>
// Komponen ini menerima 'title' sebagai sebuah properti (prop).
defineProps({
  title: String
});
</script>

<template>
  <div class="mb-16 text-center">
    <h2 class="text-4xl md:text-5xl font-black text-gray-800 mb-4">{{ title }}</h2>
    <div class="w-24 h-1.5 bg-gradient-to-r from-violet-500 to-purple-500 mx-auto rounded-full"></div>
  </div>
</template>

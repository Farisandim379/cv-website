<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import SectionTitle from './SectionTitle.vue';

// State untuk data, loading, dan error
const skills = ref([]);
const isLoading = ref(true);
const hasError = ref(false);

// Palet warna modern untuk setiap kartu skill
const colorPalette = [
  { bg: 'bg-violet-100', text: 'text-violet-800', border: 'border-violet-300', accent: 'bg-violet-500' },
  { bg: 'bg-emerald-100', text: 'text-emerald-800', border: 'border-emerald-300', accent: 'bg-emerald-500' },
  { bg: 'bg-rose-100', text: 'text-rose-800', border: 'border-rose-300', accent: 'bg-rose-500' },
  { bg: 'bg-amber-100', text: 'text-amber-800', border: 'border-amber-300', accent: 'bg-amber-500' },
  { bg: 'bg-blue-100', text: 'text-blue-800', border: 'border-blue-300', accent: 'bg-blue-500' },
  { bg: 'bg-indigo-100', text: 'text-indigo-800', border: 'border-indigo-300', accent: 'bg-indigo-500' }
];

const getSkillColor = (index) => {
  return colorPalette[index % colorPalette.length];
};

onMounted(async () => {
  try {
    const response = await axios.get('/api/skills');
    // Memastikan data yang diterima adalah array sebelum di-assign
    if (Array.isArray(response.data)) {
      skills.value = response.data;
    } else {
      throw new Error("Data yang diterima bukan array");
    }
  } catch (error) {
    console.error("Gagal mengambil data skills:", error);
    hasError.value = true;
  } finally {
    isLoading.value = false;
  }
});
</script>

<template>
  <section id="skill" class="py-24 bg-white">
    <div class="container mx-auto px-6">
      <SectionTitle title="Keahlian & Teknologi" />

      <!-- Tampilan Loading (Skeleton) -->
      <div v-if="isLoading" class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6 mt-16">
        <div v-for="n in 8" :key="n" class="bg-gray-100 rounded-2xl p-6 animate-pulse">
          <div class="h-8 w-3/4 bg-gray-200 rounded-lg mb-4"></div>
          <div class="h-4 w-1/2 bg-gray-200 rounded-lg"></div>
        </div>
      </div>

      <!-- Tampilan Error -->
      <div v-else-if="hasError" class="mt-16 text-center bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded-lg relative">
        <strong class="font-bold">Oops!</strong>
        <span class="block sm:inline"> Terjadi kesalahan saat memuat data keahlian.</span>
      </div>

      <!-- Tampilan Konten Utama -->
      <div v-else class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6 mt-16">
        <div
          v-for="(skill, index) in skills"
          :key="skill.name"
          class="relative p-6 rounded-2xl border transition-all duration-300 transform hover:-translate-y-2 hover:shadow-2xl"
          :class="[getSkillColor(index).bg, getSkillColor(index).border, `hover:shadow-[${getSkillColor(index).accent}]/20`]"
        >
          <div class="flex items-center mb-3">
            <div class="w-3 h-3 rounded-full mr-3" :class="getSkillColor(index).accent"></div>
            <h3 class="text-lg font-bold" :class="getSkillColor(index).text">{{ skill.name }}</h3>
          </div>
          <p class="text-sm" :class="getSkillColor(index).text.replace('800', '600')">{{ skill.level }}</p>
          <div class="absolute bottom-4 right-4 text-xs font-mono opacity-20" :class="getSkillColor(index).text">
            #{{ String(index + 1).padStart(2, '0') }}
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

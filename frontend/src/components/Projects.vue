<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import SectionTitle from './SectionTitle.vue';

// State untuk data, loading, dan error
const projects = ref([]);
const isLoading = ref(true);
const hasError = ref(false);

// Palet warna modern untuk setiap kartu proyek
const colorPalette = [
  { gradient: 'from-violet-600 to-purple-600', shadow: 'shadow-violet-500/25', hover: 'hover:shadow-violet-500/40' },
  { gradient: 'from-emerald-600 to-teal-600', shadow: 'shadow-emerald-500/25', hover: 'hover:shadow-emerald-500/40' },
  { gradient: 'from-rose-600 to-pink-600', shadow: 'shadow-rose-500/25', hover: 'hover:shadow-rose-500/40' },
  { gradient: 'from-amber-600 to-orange-600', shadow: 'shadow-amber-500/25', hover: 'hover:shadow-amber-500/40' }
];

const getProjectColor = (index) => {
  return colorPalette[index % colorPalette.length];
};

onMounted(async () => {
  try {
    const response = await axios.get('/api/projects');
    if (Array.isArray(response.data)) {
      projects.value = response.data;
    } else {
      throw new Error("Data proyek yang diterima bukan array");
    }
  } catch (error) {
    console.error("Gagal mengambil data proyek:", error);
    hasError.value = true;
  } finally {
    isLoading.value = false;
  }
});
</script>

<template>
  <section id="proyek" class="py-24 bg-violet-50 relative overflow-hidden">
    <!-- Elemen dekoratif latar belakang -->
    <div class="absolute inset-0 bg-[radial-gradient(circle_at_30%_20%,rgba(120,119,198,0.05),transparent)] pointer-events-none"></div>
    <div class="absolute inset-0 bg-[radial-gradient(circle_at_70%_80%,rgba(236,72,153,0.05),transparent)] pointer-events-none"></div>

    <div class="container mx-auto px-6 relative z-10">
      <SectionTitle title="Proyek Unggulan" />

      <!-- Tampilan Loading (Skeleton) -->
      <div v-if="isLoading" class="grid lg:grid-cols-2 gap-10 mt-16">
        <div v-for="n in 2" :key="n" class="bg-white/50 rounded-3xl p-8 animate-pulse">
          <div class="h-64 bg-gray-200 rounded-2xl mb-6"></div>
          <div class="h-8 w-3/4 bg-gray-200 rounded-lg mb-4"></div>
          <div class="h-4 w-full bg-gray-200 rounded-lg mb-2"></div>
          <div class="h-4 w-5/6 bg-gray-200 rounded-lg"></div>
        </div>
      </div>

      <!-- Tampilan Error -->
      <div v-else-if="hasError" class="mt-16 text-center bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded-lg relative">
        <strong class="font-bold">Oops!</strong>
        <span class="block sm:inline"> Terjadi kesalahan saat memuat data proyek.</span>
      </div>

      <!-- Tampilan Konten Utama -->
      <div v-else class="grid lg:grid-cols-2 gap-10 mt-16">
        <div
          v-for="(project, projectIndex) in projects"
          :key="project.id || project.title"
          class="group relative bg-white/80 backdrop-blur-sm rounded-3xl shadow-xl overflow-hidden border border-white/20 transform hover:scale-[1.02] transition-all duration-700 ease-out"
          :class="[getProjectColor(projectIndex).shadow, getProjectColor(projectIndex).hover]"
        >
          <div class="relative overflow-hidden">
            <img
              :src="project.image"
              :alt="project.title"
              class="w-full h-64 object-cover transform group-hover:scale-110 transition-transform duration-700 ease-out"
            />
            <div class="absolute inset-0 bg-gradient-to-t from-black/60 via-transparent to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500"></div>
          </div>
          <div class="relative p-8">
            <div class="mb-4">
              <h3 class="text-2xl font-black text-gray-800 mb-2 group-hover:text-gray-900 transition-colors duration-300">
                {{ project.title }}
              </h3>
              <div
                class="w-12 h-1 bg-gradient-to-r rounded-full transform group-hover:w-20 transition-all duration-500"
                :class="getProjectColor(projectIndex).gradient"
              ></div>
            </div>
            <p class="text-gray-600 mb-6 leading-relaxed line-clamp-3">
              {{ project.description }}
            </p>
            <div class="mb-6">
              <h4 class="text-sm font-semibold text-gray-500 mb-3 uppercase tracking-wide">Tech Stack</h4>
              <div class="flex flex-wrap gap-2">
                <span
                  v-for="(tech, techIndex) in project.tech"
                  :key="tech"
                  class="inline-flex items-center px-3 py-1.5 rounded-full text-xs font-bold text-white shadow-lg transform hover:scale-105 transition-all duration-300 cursor-pointer bg-gradient-to-r"
                  :class="getProjectColor(techIndex).gradient"
                >
                  <span class="w-2 h-2 bg-white/30 rounded-full mr-2"></span>
                  {{ tech }}
                </span>
              </div>
            </div>
            <div class="flex items-center justify-between">
              <a
                :href="project.link"
                target="_blank"
                rel="noopener noreferrer"
                class="group/btn inline-flex items-center px-6 py-3 bg-gradient-to-r text-white font-semibold rounded-full shadow-lg hover:shadow-xl transform hover:scale-105 transition-all duration-300"
                :class="getProjectColor(projectIndex).gradient"
              >
                <span class="mr-2">Lihat Detail</span>
                <svg class="w-4 h-4 transform group-hover/btn:translate-x-1 transition-transform duration-300" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3"></path></svg>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* Utilitas untuk memotong teks jika terlalu panjang */
.line-clamp-3 {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import SectionTitle from './SectionTitle.vue';

// State untuk data, loading, dan error
const educationHistory = ref([]);
const isLoading = ref(true);
const hasError = ref(false);

// Fungsi untuk menentukan warna timeline
const getTimelineColor = (index) => {
  const colors = [
    { border: 'border-violet-300', bg: 'bg-violet-500', text: 'text-violet-600', dot: 'bg-violet-100', shadow: 'shadow-violet-200' },
    { border: 'border-emerald-300', bg: 'bg-emerald-500', text: 'text-emerald-600', dot: 'bg-emerald-100', shadow: 'shadow-emerald-200' },
    { border: 'border-rose-300', bg: 'bg-rose-500', text: 'text-rose-600', dot: 'bg-rose-100', shadow: 'shadow-rose-200' },
    { border: 'border-blue-300', bg: 'bg-blue-500', text: 'text-blue-600', dot: 'bg-blue-100', shadow: 'shadow-blue-200' }
  ];
  return colors[index % colors.length];
};

onMounted(async () => {
  try {
    const response = await axios.get('/api/education');
    if (Array.isArray(response.data)) {
      educationHistory.value = response.data;
    } else {
      throw new Error("Data pendidikan yang diterima bukan array");
    }
  } catch (error) {
    console.error("Gagal mengambil data pendidikan:", error);
    hasError.value = true;
  } finally {
    isLoading.value = false;
  }
});
</script>

<template>
  <section id="pendidikan" class="py-24 bg-gradient-to-br from-slate-50 to-white">
    <div class="container mx-auto px-6">
      <SectionTitle title="Riwayat Pendidikan" />

      <!-- Tampilan Loading (Skeleton) -->
      <div v-if="isLoading" class="mt-16 relative w-full max-w-4xl mx-auto">
        <!-- ... (kode skeleton tetap sama) ... -->
      </div>

      <!-- Tampilan Error -->
      <div v-else-if="hasError" class="mt-16 text-center max-w-md mx-auto">
        <!-- ... (kode error tetap sama) ... -->
      </div>

      <!-- Tampilan Konten Utama dengan STRUKTUR YANG DIPERBAIKI -->
      <div v-else class="mt-16 relative w-full max-w-4xl mx-auto">
        <!-- Garis timeline vertikal -->
        <div class="absolute left-1/2 top-5 bottom-5 w-px bg-gray-200 -translate-x-1/2"></div>

        <!-- Perulangan untuk setiap item pendidikan -->
        <div v-for="(edu, index) in educationHistory" :key="edu.id" class="relative mb-8 flex items-center">

          <!-- KOLOM KIRI -->
          <div class="w-1/2 pr-8">
            <div v-if="index % 2 === 0" class="text-right">
              <div class="bg-white rounded-xl p-6 shadow-sm border border-gray-100 transition-all duration-300 hover:shadow-lg hover:border-gray-200 hover:-translate-y-1">
                <div class="inline-flex items-center px-3 py-1 rounded-full text-xs font-semibold mb-3" :class="[getTimelineColor(index).text, getTimelineColor(index).dot]">
                  {{ edu.period }}
                </div>
                <h3 class="text-xl font-bold text-gray-800 mb-1">{{ edu.institution }}</h3>
                <p class="text-gray-600 font-medium">{{ edu.major }}</p>
              </div>
            </div>
          </div>

          <!-- Titik pada timeline -->
          <div class="absolute left-1/2 w-10 h-10 rounded-full border-4 z-10 bg-white -translate-x-1/2 shadow-lg" :class="getTimelineColor(index).border">
            <div class="w-full h-full rounded-full" :class="getTimelineColor(index).bg"></div>
          </div>

          <!-- KOLOM KANAN -->
          <div class="w-1/2 pl-8">
            <div v-if="index % 2 !== 0" class="text-left">
               <div class="bg-white rounded-xl p-6 shadow-sm border border-gray-100 transition-all duration-300 hover:shadow-lg hover:border-gray-200 hover:-translate-y-1">
                <div class="inline-flex items-center px-3 py-1 rounded-full text-xs font-semibold mb-3" :class="[getTimelineColor(index).text, getTimelineColor(index).dot]">
                  {{ edu.period }}
                </div>
                <h3 class="text-xl font-bold text-gray-800 mb-1">{{ edu.institution }}</h3>
                <p class="text-gray-600 font-medium">{{ edu.major }}</p>
              </div>
            </div>
          </div>

        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* Style tambahan bisa ditambahkan di sini jika perlu */
</style>

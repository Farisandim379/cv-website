<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

// State untuk membuka/menutup menu mobile
const isMenuOpen = ref(false);
// State untuk melacak seksi mana yang sedang aktif di layar
const activeSection = ref('profil');

// Daftar link untuk navigasi
const navLinks = [
  { id: 'profil', name: 'Home' },
  { id: 'pendidikan', name: 'Education' },
  { id: 'skill', name: 'Skill' },
  { id: 'proyek', name: 'Project' },
  { id: 'kontak', name: 'Contact Us' }
];

// Fungsi untuk menutup menu mobile (berguna saat link di klik)
const closeMenu = () => {
  isMenuOpen.value = false;
};

// Fungsi untuk menangani scroll dan menentukan seksi aktif
const handleScroll = () => {
  const sections = navLinks.map(link => document.getElementById(link.id));
  const scrollPosition = window.scrollY + 150; // Offset 150px untuk akurasi yang lebih baik

  for (const section of sections) {
    if (section && scrollPosition >= section.offsetTop && scrollPosition < section.offsetTop + section.offsetHeight) {
      activeSection.value = section.id;
      return;
    }
  }
};

// Menambahkan event listener saat komponen dimuat
onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

// Menghapus event listener saat komponen dihancurkan untuk mencegah memory leak
onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<template>
  <header class="bg-white/80 backdrop-blur-sm shadow-md sticky top-0 z-50 transition-all duration-300">
    <nav class="container mx-auto px-6 py-4 flex justify-between items-center">
      <!-- Logo / Nama Pengguna -->
      <a href="#profil" class="text-xl font-bold text-gray-800 hover:text-violet-600 transition-colors">
        Faris Andi Muhammad
      </a>

      <!-- Menu untuk Desktop -->
      <ul class="hidden md:flex space-x-8 items-center">
        <li v-for="link in navLinks" :key="link.id">
          <a
            :href="`#${link.id}`"
            class="relative font-medium text-gray-600 hover:text-violet-600 transition-colors duration-300"
            :class="{ 'text-violet-600': activeSection === link.id }"
          >
            {{ link.name }}
            <!-- Indikator titik di bawah menu yang aktif -->
            <span
              class="absolute -bottom-2 left-1/2 w-2 h-2 bg-violet-500 rounded-full transform -translate-x-1/2 transition-all duration-300"
              :class="activeSection === link.id ? 'opacity-100 scale-100' : 'opacity-0 scale-0'"
            ></span>
          </a>
        </li>
      </ul>

      <!-- Tombol Menu untuk Mobile -->
      <div class="md:hidden">
        <button @click="isMenuOpen = !isMenuOpen" class="text-gray-800 focus:outline-none" aria-label="Buka menu">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <!-- Ikon hamburger -->
            <path v-if="!isMenuOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path>
            <!-- Ikon silang (X) -->
            <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
          </svg>
        </button>
      </div>
    </nav>

    <!-- Menu Dropdown untuk Mobile -->
    <div v-if="isMenuOpen" class="md:hidden bg-white/95 backdrop-blur-sm shadow-lg absolute top-full left-0 w-full">
      <ul class="flex flex-col items-center space-y-4 py-6">
        <li v-for="link in navLinks" :key="link.id">
          <a
            :href="`#${link.id}`"
            @click="closeMenu"
            class="text-lg font-medium text-gray-700 hover:text-violet-600 transition-colors"
            :class="{ 'text-violet-600': activeSection === link.id }"
          >
            {{ link.name }}
          </a>
        </li>
      </ul>
    </div>
  </header>
</template>

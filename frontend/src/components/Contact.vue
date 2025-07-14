<script setup>
// Komponen SectionTitle sudah tidak digunakan di sini, bisa dihapus jika tidak ada keperluan lain.
// import SectionTitle from './SectionTitle.vue';
</script>

<template>
  <div class="bg-violet-50">
    <div class="wave-container">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 320" class="block">
        <path fill="#1e293b" fill-opacity="1" d="M0,160L48,176C96,192,192,224,288,213.3C384,203,480,149,576,138.7C672,128,768,160,864,186.7C960,213,1056,235,1152,218.7C1248,203,1344,149,1392,122.7L1440,96L1440,320L1392,320C1344,320,1248,320,1152,320C1056,320,960,320,864,320C768,320,672,320,576,320C480,320,384,320,288,320C192,320,96,320,48,320L0,320Z"></path>
      </svg>
    </div>

    <footer id="kontak" class="relative py-20 bg-slate-900 text-white overflow-hidden">
      <div class="absolute inset-0 bg-[radial-gradient(circle_at_25%_25%,rgba(139,92,246,0.1),transparent_40%)] pointer-events-none"></div>
      <div class="absolute inset-0 bg-[radial-gradient(circle_at_75%_75%,rgba(168,85,247,0.1),transparent_40%)] pointer-events-none"></div>

      <div class="container mx-auto px-6 text-center relative z-10">

        <div class="max-w-2xl mx-auto bg-slate-800/50 p-8 md:p-12 rounded-3xl border border-slate-700">

          <div class="mb-4">
            <h2 class="text-3xl md:text-4xl font-black text-white">Hubungi Saya</h2>
            <div class="w-20 h-1 bg-gradient-to-r from-violet-500 to-purple-500 mx-auto mt-4 rounded-full"></div>
          </div>

          <p class="text-lg md:text-xl text-gray-300 mt-4 mb-8">
            Saya selalu terbuka untuk diskusi, kolaborasi, atau sekadar bertukar sapa. Jangan ragu untuk terhubung.
          </p>
          <a href="mailto:farisandim@gmail.com" class="inline-block font-bold rounded-full text-white bg-gradient-to-r from-violet-600 to-purple-600 py-3 px-8 shadow-lg hover:shadow-xl hover:scale-105 transform transition-all duration-300">
            Kirim Email
          </a>
        </div>

        <div class="flex justify-center space-x-6 my-12">
          <a href="https://github.com/Farisandim379" target="_blank" rel="noopener noreferrer" class="social-icon group">
            <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
              <path fill-rule="evenodd" d="M12 2C6.477 2 2 6.477 2 12c0 4.418 2.865 8.168 6.839 9.49.5.092.682-.217.682-.482 0-.237-.009-.868-.014-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.031-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.378.203 2.398.1 2.651.64.7 1.03 1.595 1.03 2.688 0 3.848-2.338 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.001 10.001 0 0022 12c0-5.523-4.477-10-10-10z" clip-rule="evenodd" />
            </svg>
          </a>
          <a href="https://www.linkedin.com/in/faris-andi-muhammad-5200ba2b9/" target="_blank" rel="noopener noreferrer" class="social-icon group">
            <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
              <path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"/>
            </svg>
          </a>
        </div>

        <div class="border-t border-slate-800 pt-8 text-gray-500 flex items-center justify-center space-x-2">
          <span>&copy; {{ new Date().getFullYear() }} Dibuat dengan</span>
          <svg class="w-5 h-5 text-red-500 animate-pulse-heart" fill="currentColor" viewBox="0 0 20 20">
            <path fill-rule="evenodd" d="M3.172 5.172a4 4 0 015.656 0L10 6.343l1.172-1.171a4 4 0 115.656 5.656L10 17.657l-6.828-6.829a4 4 0 010-5.656z" clip-rule="evenodd"></path>
          </svg>
          <span>oleh Faris Andi Muhammad</span>
        </div>
      </div>
    </footer>
  </div>
</template>

<style scoped>
/* Ini memastikan wave SVG menempel di bawah tanpa ada celah */
.wave-container {
  line-height: 0;
}

.social-icon {
  @apply flex items-center justify-center w-12 h-12 bg-slate-800 rounded-full text-gray-400 transition-all duration-300;
}

.social-icon:hover {
  @apply text-white bg-gradient-to-br from-violet-600 to-purple-500 scale-110 shadow-lg;
}

/* Animasi untuk ikon hati */
@keyframes pulse-heart {
  50% {
    transform: scale(1.2);
  }
}
.animate-pulse-heart {
  animation: pulse-heart 1.5s ease-in-out infinite;
}
</style>

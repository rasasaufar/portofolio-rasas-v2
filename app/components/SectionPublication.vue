<template>
  <section id="publication" class="py-24 relative">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Section Header -->
      <div class="text-center mb-16 animate-on-scroll">
        <span class="badge mb-4">Publications</span>
        <h2 class="section-title">Research and Publications</h2>
        <p class="section-subtitle">Berikut adalah jurnal ilmiah yang telah saya publikasikan</p>
      </div>

      <!-- Publications List -->
      <div class="space-y-6 max-w-4xl mx-auto">
        <div
          v-for="(pub, index) in publications"
          :key="pub.title"
          class="glass-card-solid p-6 md:p-8 card-hover animate-on-scroll group"
          :style="{ animationDelay: `${index * 0.1}s` }"
        >
          <div class="flex gap-5">
            <!-- Index Number -->
            <div class="hidden sm:flex flex-shrink-0 w-14 h-14 rounded-2xl bg-gradient-to-br from-lavender-100 to-pastel-100 dark:from-lavender-900/40 dark:to-pastel-900/40 items-center justify-center border border-lavender-200/30 dark:border-lavender-800/30">
              <span class="text-xl font-bold bg-gradient-to-br from-lavender-600 to-pastel-500 dark:from-lavender-400 dark:to-pastel-300 bg-clip-text text-transparent">
                {{ String(index + 1).padStart(2, '0') }}
              </span>
            </div>

            <div class="flex-1 space-y-3">
              <!-- Title -->
              <h3 class="text-lg font-bold text-gray-800 dark:text-gray-100 group-hover:text-lavender-700 dark:group-hover:text-lavender-400 transition-colors duration-300 leading-snug">
                {{ pub.title }}
              </h3>

              <!-- Meta -->
              <div class="flex flex-wrap items-center gap-3 text-xs text-gray-500 dark:text-gray-400">
                <span class="flex items-center gap-1">
                  <svg class="w-3.5 h-3.5 text-lavender-400 dark:text-lavender-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253" />
                  </svg>
                  {{ pub.journal }}
                </span>
                <span class="w-1 h-1 rounded-full bg-gray-300 dark:bg-gray-600"></span>
                <span class="flex items-center gap-1">
                  <svg class="w-3.5 h-3.5 text-lavender-400 dark:text-lavender-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
                  </svg>
                  {{ pub.year }}
                </span>
                <span class="w-1 h-1 rounded-full bg-gray-300 dark:bg-gray-600"></span>
                <span
                  class="inline-flex items-center gap-1 px-2 py-0.5 rounded-full text-xs font-medium"
                  :class="pub.status === 'Published'
                    ? 'bg-green-50 dark:bg-green-900/20 text-green-700 dark:text-green-400 border border-green-100 dark:border-green-800/50'
                    : 'bg-yellow-50 dark:bg-yellow-900/20 text-yellow-700 dark:text-yellow-400 border border-yellow-100 dark:border-yellow-800/50'"
                >
                  {{ pub.status }}
                </span>
              </div>

              <!-- Authors -->
              <p class="text-sm text-gray-500 dark:text-gray-400">
                <span class="font-medium text-lavender-600 dark:text-lavender-400">Authors: </span>{{ pub.authors }}
              </p>

              <!-- Abstract -->
              <p class="text-sm text-gray-500 dark:text-gray-400 leading-relaxed">{{ pub.abstract }}</p>

              <!-- Tags & Link -->
              <div class="flex items-center justify-between pt-2">
                <div class="flex flex-wrap gap-1.5">
                  <span v-for="tag in pub.tags" :key="tag" class="px-2 py-0.5 text-xs rounded-md bg-lavender-50 dark:bg-lavender-900/30 text-lavender-600 dark:text-lavender-300 border border-lavender-100/40 dark:border-lavender-800/40">
                    {{ tag }}
                  </span>
                </div>

                <a
                  v-if="pub.doi"
                  :href="pub.doi"
                  target="_blank"
                  rel="noopener noreferrer"
                  class="flex items-center gap-1 text-xs font-medium text-lavender-500 hover:text-lavender-700 transition-colors group/link"
                >
                  <span>View Paper</span>
                  <svg class="w-3.5 h-3.5 group-hover/link:translate-x-0.5 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
                  </svg>
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
const publications = [
  {
    title: 'Analisis Pengujian Pengembangan Sistem Informasi Geografis Daerah Rawan Rob Di Kota Pekalongan',
    journal: 'Jurnal Sains Komputer & Informatika (J-SAKTI)',
    year: 'Maret 2023',
    status: 'Published',
    authors: 'Mohammad Rasas Aufar, Pradana Ananda Raharja',
    abstract: 'Penelitian ini menerapkan metode Agile dalam mendesain Sistem Informasi Geografis (SIG) untuk memetakan kawasan rawan bencana banjir rob di pesisir utara Kota Pekalongan. Integrasi teknologi SIG dirancang untuk memberikan kemudahan dalam mengidentifikasi tingkat kerentanan wilayah dan menyajikan data ancaman gelombang pasang kepada masyarakat maupun pihak terkait secara visual dan akurat.',
    tags: ['Sistem Informasi Geografis', 'Agile Method', 'Banjir Rob', 'Pemetaan Wilayah'],
    doi: 'https://garuda.kemdiktisaintek.go.id/documents/detail/3418708',
  },
]
</script>

<template>
  <section id="portfolio" class="py-24 relative">
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Section Header -->
      <div class="text-center mb-16 animate-on-scroll">
        <span class="badge mb-4">Portfolio</span>
        <h2 class="section-title">Work and Experience</h2>
        <p class="section-subtitle">Professional experiences and projects that showcase my skills</p>
      </div>

      <!-- Tab Switcher -->
      <div class="flex justify-center mb-12 animate-on-scroll">
        <div class="inline-flex p-1.5 rounded-2xl bg-white/60 dark:bg-gray-800/60 border border-lavender-100/40 dark:border-gray-700/50 backdrop-blur-sm shadow-sm">
          <button
            v-for="tab in tabs"
            :key="tab.id"
            class="px-6 py-2.5 rounded-xl text-sm font-medium transition-all duration-300"
            :class="activeTab === tab.id
              ? 'bg-gradient-to-r from-lavender-500 to-pastel-500 text-white shadow-md shadow-lavender-200/50 dark:shadow-lavender-900/30'
              : 'text-gray-500 dark:text-gray-400 hover:text-lavender-600 dark:hover:text-lavender-400'"
            @click="activeTab = tab.id"
          >
            {{ tab.label }}
          </button>
        </div>
      </div>

      <!-- Work Experience -->
      <!-- Experience Tab -->
      <div v-if="activeTab === 'experience'" class="space-y-8">
          <div
            v-for="(exp, index) in experiences"
            :key="exp.company"
            class="glass-card-solid p-6 md:p-8 card-hover animate-fade-in-up"
            :style="{ animationDelay: `${index * 0.1}s` }"
          >
            <div class="flex flex-col md:flex-row gap-6">
              <!-- Company Info -->
              <div class="md:w-1/3 space-y-3">
                <div v-if="exp.logo" class="w-16 h-16 rounded-xl bg-white border border-lavender-100 flex items-center justify-center overflow-hidden p-1 shadow-sm">
                  <img :src="exp.logo" :alt="exp.company" class="w-full h-full object-contain" />
                </div>
                <div v-else class="w-16 h-16 rounded-xl bg-gradient-to-br from-lavender-100 to-pastel-100 dark:from-lavender-900/40 dark:to-pastel-900/40 flex items-center justify-center">
                  <span class="text-2xl">{{ exp.emoji }}</span>
                </div>
                <h3 class="text-lg font-bold text-gray-800 dark:text-gray-100">{{ exp.company }}</h3>
                <p class="text-sm font-medium text-lavender-600 dark:text-lavender-400">{{ exp.position }}</p>
                <p class="text-xs text-gray-400 dark:text-gray-500">{{ exp.period }}</p>
                <div class="flex flex-wrap gap-1.5">
                  <span v-for="tech in exp.tech" :key="tech" class="px-2 py-0.5 text-xs rounded-md bg-lavender-50 dark:bg-lavender-900/30 text-lavender-600 dark:text-lavender-300 border border-lavender-100/40 dark:border-lavender-800/40">
                    {{ tech }}
                  </span>
                </div>
              </div>

              <!-- Description & Gallery -->
              <div class="md:w-2/3 space-y-4">
                <p class="text-gray-600 dark:text-gray-400 leading-relaxed text-sm">{{ exp.description }}</p>

                <ul class="space-y-2">
                  <li v-for="resp in exp.responsibilities" :key="resp" class="flex items-start gap-2 text-sm text-gray-500 dark:text-gray-400">
                    <svg class="w-4 h-4 text-lavender-400 dark:text-lavender-500 mt-0.5 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                    </svg>
                    {{ resp }}
                  </li>
                </ul>

                <!-- Gallery -->
                <div v-if="exp.gallery && exp.gallery.length > 0" class="pt-2">
                  <p class="text-xs font-medium text-gray-400 dark:text-gray-500 uppercase tracking-wider mb-3">Project Gallery</p>
                  <div class="grid grid-cols-2 sm:grid-cols-3 gap-3">
                    <div
                      v-for="(img, imgIndex) in exp.gallery"
                      :key="imgIndex"
                      class="relative aspect-video rounded-xl overflow-hidden border border-lavender-100/40 dark:border-gray-700/50 group cursor-pointer"
                      @click="openGallery(index, imgIndex)"
                    >
                      <img v-if="img.image" :src="img.image" :alt="img.caption" class="w-full h-full object-cover" />
                      <div v-else class="w-full h-full bg-gradient-to-br from-lavender-100 to-pastel-100 dark:from-lavender-900/40 dark:to-pastel-900/40 flex items-center justify-center">
                        <span class="text-3xl">{{ img.emoji }}</span>
                      </div>
                      <div class="absolute inset-0 bg-lavender-900/60 opacity-0 group-hover:opacity-100 transition-all duration-300 flex items-center justify-center">
                        <svg class="w-6 h-6 text-white mb-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0zM10 7v3m0 0v3m0-3h3m-3 0H7" />
                        </svg>
                        <p class="text-white text-xs font-medium px-3 text-center">{{ img.caption }}</p>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Projects Tab -->
        <div v-else class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <div
            v-for="(project, index) in projects"
            :key="project.name"
            class="glass-card-solid overflow-hidden card-hover animate-fade-in-up"
            :style="{ animationDelay: `${index * 0.1}s` }"
          >
            <!-- Project Thumbnail -->
            <div class="aspect-video bg-gradient-to-br from-lavender-100 to-pastel-100 dark:from-lavender-900/40 dark:to-pastel-900/40 flex items-center justify-center relative overflow-hidden group">
              <img v-if="project.image" :src="project.image" :alt="project.name" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500" />
              <span v-else class="text-5xl group-hover:scale-125 transition-transform duration-500">{{ project.emoji }}</span>
              <div class="absolute inset-0 bg-gradient-to-t from-white/80 dark:from-gray-900/80 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
            </div>

            <div class="p-6 space-y-3">
              <div class="flex items-start justify-between gap-2">
                <h3 class="font-bold text-gray-800 dark:text-gray-100">{{ project.name }}</h3>
                <span class="badge whitespace-nowrap">{{ project.type }}</span>
              </div>

              <p class="text-sm text-gray-500 dark:text-gray-400 leading-relaxed">{{ project.description }}</p>

              <div class="flex flex-wrap gap-1.5 pt-1">
                <span v-for="tech in project.tech" :key="tech" class="px-2 py-0.5 text-xs rounded-md bg-lavender-50 dark:bg-lavender-900/30 text-lavender-600 dark:text-lavender-300 border border-lavender-100/40 dark:border-lavender-800/40">
                  {{ tech }}
                </span>
              </div>

              <div class="flex gap-3 pt-3 border-t border-lavender-100/40 dark:border-gray-700/50">
                <a v-if="project.demo" :href="project.demo" target="_blank" class="text-xs font-medium text-lavender-600 dark:text-lavender-400 hover:text-lavender-800 dark:hover:text-lavender-300 transition-colors flex items-center gap-1">
                  <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
                  </svg>
                  Live Demo
                </a>
                <a v-if="project.github" :href="project.github" target="_blank" class="text-xs font-medium text-gray-400 dark:text-gray-500 hover:text-gray-600 dark:hover:text-gray-400 transition-colors flex items-center gap-1">
                  <svg class="w-3.5 h-3.5" fill="currentColor" viewBox="0 0 24 24">
                    <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
                  </svg>
                  Source
                </a>
              </div>
            </div>
          </div>
        </div>
    </div>

    <!-- Gallery Popup Modal -->
    <Teleport to="body">
      <Transition name="gallery-modal">
        <div
          v-if="galleryOpen"
          class="fixed inset-0 z-[9999] flex items-center justify-center"
          @click.self="closeGallery"
          @keydown.escape="closeGallery"
          @keydown.left="prevImage"
          @keydown.right="nextImage"
        >
          <!-- Backdrop -->
          <div class="absolute inset-0 bg-black/80 backdrop-blur-md" @click="closeGallery"></div>

          <!-- Modal Content -->
          <div class="relative z-10 w-full max-w-3xl mx-4 sm:mx-8">
            <!-- Close Button -->
            <button
              class="absolute -top-12 right-0 sm:-right-2 w-10 h-10 rounded-full bg-white/10 hover:bg-white/20 border border-white/20 text-white flex items-center justify-center transition-all duration-300 hover:scale-110 hover:rotate-90"
              @click="closeGallery"
            >
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>

            <!-- Image Container -->
            <div class="relative rounded-2xl overflow-hidden bg-gray-900/90 border border-white/10 shadow-2xl shadow-black/50">
              <!-- Image Display -->
              <div class="aspect-video flex items-center justify-center relative">
                <Transition :name="slideDirection" mode="out-in">
                  <div
                    :key="currentImageIndex"
                    class="w-full h-full flex flex-col items-center justify-center"
                    :class="currentGalleryImage?.image ? '' : 'bg-gradient-to-br from-lavender-200 to-pastel-200 dark:from-lavender-900/60 dark:to-pastel-900/60'"
                  >
                    <img v-if="currentGalleryImage?.image" :src="currentGalleryImage.image" :alt="currentGalleryImage.caption" class="w-full h-full object-cover" />
                    <span v-else class="text-7xl sm:text-8xl mb-4 drop-shadow-lg animate-bounce-slow">{{ currentGalleryImage?.emoji }}</span>
                  </div>
                </Transition>
              </div>

              <!-- Bottom Info Bar -->
              <div class="px-6 py-4 bg-gradient-to-t from-black/60 to-transparent">
                <div class="flex items-start justify-between gap-4">
                  <div class="flex-1 min-w-0">
                    <p class="text-white font-semibold text-sm sm:text-base">{{ currentGalleryImage?.caption }}</p>
                    <p class="text-white/50 text-xs mt-0.5">{{ currentExperienceCompany }}</p>
                  </div>
                  <div class="flex items-center gap-1.5 mt-1">
                    <span
                      v-for="(_, dotIndex) in currentGallery"
                      :key="dotIndex"
                      class="w-2 h-2 rounded-full transition-all duration-300"
                      :class="dotIndex === currentImageIndex
                        ? 'bg-white scale-110 shadow-lg shadow-white/30'
                        : 'bg-white/30 hover:bg-white/50'"
                    ></span>
                  </div>
                </div>
                <p v-if="currentGalleryImage?.description" class="text-white/60 text-xs sm:text-sm mt-2 leading-relaxed">
                  {{ currentGalleryImage.description }}
                </p>
              </div>
            </div>

            <!-- Navigation Arrows -->
            <button
              v-if="currentGallery && currentGallery.length > 1"
              class="absolute -left-16 sm:-left-20 top-1/2 -translate-y-1/2 w-12 h-12 rounded-full bg-white/10 hover:bg-white/25 border border-white/20 text-white flex items-center justify-center transition-all duration-300 hover:scale-110 group"
              @click="prevImage"
            >
              <svg class="w-5 h-5 group-hover:-translate-x-0.5 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M15 19l-7-7 7-7" />
              </svg>
            </button>
            <button
              v-if="currentGallery && currentGallery.length > 1"
              class="absolute -right-16 sm:-right-20 top-1/2 -translate-y-1/2 w-12 h-12 rounded-full bg-white/10 hover:bg-white/25 border border-white/20 text-white flex items-center justify-center transition-all duration-300 hover:scale-110 group"
              @click="nextImage"
            >
              <svg class="w-5 h-5 group-hover:translate-x-0.5 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M9 5l7 7-7 7" />
              </svg>
            </button>

            <!-- Counter -->
            <div class="absolute -bottom-10 left-1/2 -translate-x-1/2 text-white/40 text-xs font-medium tracking-wider">
              {{ currentImageIndex + 1 }} / {{ currentGallery?.length || 0 }}
            </div>
          </div>
        </div>
      </Transition>
    </Teleport>
  </section>
</template>

<script setup lang="ts">
const activeTab = ref('experience')

// Gallery popup state
const galleryOpen = ref(false)
const currentExperienceIndex = ref(0)
const currentImageIndex = ref(0)
const slideDirection = ref('slide-right')

const currentGallery = computed(() => {
  if (currentExperienceIndex.value >= 0 && currentExperienceIndex.value < experiences.length) {
    return experiences[currentExperienceIndex.value]!.gallery
  }
  return []
})

const currentGalleryImage = computed(() => {
  if (currentGallery.value && currentImageIndex.value >= 0 && currentImageIndex.value < currentGallery.value.length) {
    return currentGallery.value[currentImageIndex.value]
  }
  return null
})

const currentExperienceCompany = computed(() => {
  if (currentExperienceIndex.value >= 0 && currentExperienceIndex.value < experiences.length) {
    return experiences[currentExperienceIndex.value]!.company
  }
  return ''
})

function openGallery(expIndex: number, imgIndex: number) {
  currentExperienceIndex.value = expIndex
  currentImageIndex.value = imgIndex
  galleryOpen.value = true
  document.body.style.overflow = 'hidden'
  nextTick(() => {
    window.addEventListener('keydown', handleKeydown)
  })
}

function closeGallery() {
  galleryOpen.value = false
  document.body.style.overflow = ''
  window.removeEventListener('keydown', handleKeydown)
}

function prevImage() {
  if (currentGallery.value && currentGallery.value.length > 1) {
    slideDirection.value = 'slide-left'
    currentImageIndex.value = currentImageIndex.value <= 0
      ? currentGallery.value.length - 1
      : currentImageIndex.value - 1
  }
}

function nextImage() {
  if (currentGallery.value && currentGallery.value.length > 1) {
    slideDirection.value = 'slide-right'
    currentImageIndex.value = currentImageIndex.value >= currentGallery.value.length - 1
      ? 0
      : currentImageIndex.value + 1
  }
}

function handleKeydown(e: KeyboardEvent) {
  if (e.key === 'Escape') closeGallery()
  if (e.key === 'ArrowLeft') prevImage()
  if (e.key === 'ArrowRight') nextImage()
}

onUnmounted(() => {
  window.removeEventListener('keydown', handleKeydown)
  document.body.style.overflow = ''
})

const tabs = [
  { id: 'experience', label: '💼 Work Experience' },
  { id: 'projects', label: '🚀 Projects' },
]

const experiences = [
  {
    company: 'PT. Traspac Makmur Sejahtera',
    position: 'IT Implementation',
    period: 'Aug 2024 - Present',
    emoji: '🏢',
    logo: 'https://karir.traspac.id/assets/img/logotraspac.png',
    description: 'Menjadi IT Implementor, IT Infrastructure dan Data Analis. Menghandle beberapa project di Kementerian dan Militer.',
    responsibilities: [
      'Kemenlu RI — Bekerja onsite bersama Subdit SISTIK Direktorat PWNI, memberikan dukungan teknis pengembangan situs web "Safe Travel" dan manajemen infrastruktur server "Portal Peduli WNI" menggunakan Ubuntu',
      'Kemenlu RI — Menyiapkan dokumentasi teknis bulanan (laporan pemeliharaan, analisis bug, panduan pemecahan masalah, dan manajemen permintaan perubahan)',
      'Mabes TNI — Mengelola operasi basis data penting, termasuk pencadangan dan pemulihan rutin di lingkungan produksi untuk memastikan integritas data',
      'Mabes TNI — Menerapkan penerapan aplikasi Sisfopajak pada infrastruktur server fisik serta melakukan pengujian fungsional dan verifikasi komprehensif pasca-penerapan',
      'Mabes TNI — Menjadi Presenter Pelatihan Aplikasi Sistem Data Alutsista dan Pendukungnya di Mabes TNI, Mabes AL, dan Pusdatin Kementerian Pertahanan',
      'Kementerian Hilirisasi dan Investasi — Mengelola Sistem Presensi di Kepegawaian BKPM',
    ],
    tech: ['Ubuntu', 'Server Infrastructure', 'Database Management', 'Application Deployment'],
    gallery: [
      { image: '/images/gallery/traspac-kemenlu.png', emoji: '', caption: 'Kementerian Luar Negeri RI', description: 'Kegiatan dukungan teknis dan bimbingan teknis bersama Subdit SISTIK Direktorat PWNI di Kementerian Luar Negeri Republik Indonesia.' },
      { image: '/images/gallery/traspac-kemhan.png', emoji: '', caption: 'Pusdatin Kemhan RI', description: 'Menjadi presenter pelatihan aplikasi Sistem Data Alutsista dan Pendukungnya di Pusat Data dan Informasi Kementerian Pertahanan Republik Indonesia.' },
    ],
  },
  {
    company: 'PT. Metro Network Solutions',
    position: 'Operator Scanner',
    period: 'Sep 2023 - Dec 2023',
    emoji: '🖨️',
    logo: 'https://media.licdn.com/dms/image/v2/C560BAQHq1FwKfCDJZA/company-logo_200_200/company-logo_200_200/0/1667985560103/pt_metronet_logo?e=2147483647&v=beta&t=gsRuAkezzvj65j2AGShob4KmQDCnAjpuGbO4YH5xGZE',
    description: 'Menjadi bagian dari tim pelaksana proyek Digitalisasi Arsip di Badan Pertanahan Nasional (BPN) Kota Pekalongan untuk mendukung transformasi data fisik ke digital.',
    responsibilities: [
      'Bekerja pada proyek Digitalisasi di Kantor Badan Pertanahan Nasional (BPN) Kota Pekalongan',
      'Menyortir dan merapikan berbagai album dan dokumen fisik dengan teliti sebelum proses digitalisasi',
      'Melakukan pemindaian (scanning) dokumen dalam jumlah besar per harinya untuk persiapan pengarsipan',
      'Mengedit dan mengoptimalkan hasil scan menggunakan perangkat lunak NAPS2 agar tajam, lurus, dan mudah dibaca',
      'Bekerja dengan disiplin tinggi di bawah tekanan untuk selalu mencapai target pemindaian maupun tenggat waktu',
      'Menjaga kelengkapan, kerahasiaan, dan integritas dokumen-dokumen tanah yang bernilai tinggi selama project berlangsung',
    ],
    tech: ['NAPS2', 'Document Editing', 'Data Management', 'Scanner Handling'],
    gallery: [
      { image: '/images/gallery/bpn-closing.jpeg', emoji: '📸', caption: 'Penutupan Project', description: 'Momen kebersamaan foto dengan seluruh tim pelaksana pada penghujung masa proyek Digitalisasi Arsip BPN Kota Pekalongan setelah berhasil menyelesaikan seluruh target pemindaian.' },
    ],
  },
  {
    company: 'Niagahoster - Web Hosting Unlimited Indonesia',
    position: 'Project-Based Virtual Intern : UI / UX Designer',
    period: 'Jul 2023 - Aug 2023',
    emoji: '🌐',
    logo: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRVYFavWOvYAbq_z018Y5-cZNuutUC_256vVw&s',
    description: 'Project-Based Virtual Internship bersama Rakamin Academy (Niagahoster x Rakamin Academy).',
    responsibilities: [
      'Menyelesaikan berbagai tugas yang berkaitan dengan aktivitas UI/UX Designer dari Niagahoster',
      'Merancang antarmuka pengguna (User Interface) dan pengalaman pengguna (User Experience)',
      'Membuat wireframe dan prototipe interaktif untuk memvisualisasikan alur penggunaan (seperti Checkout Flow)',
    ],
    tech: ['User Experience (UX)', 'Prototyping', 'User Interface', 'Wireframing'],
    gallery: [
      { image: '/images/gallery/Niagahoster.png', emoji: '🛒', caption: 'Checkout Flow', description: 'Hasil desain alur antarmuka pengguna (Checkout Flow) website Niagahoster yang dirancang ulang untuk memberikan pengalaman berbelanja dan pembayaran yang aman, mudah dicerna, dan efisien bagi pengguna.' },
      { image: '/images/gallery/5.png', emoji: '📜', caption: 'Certificate of Completion', description: 'Sertifikat kelulusan resmi yang memvalidasi pencapaian, keberhasilan, serta pengembangan keterampilan esensial sebagai UI/UX Designer selama program Virtual Internship.' },
    ],
  },
  {
    company: 'Nuri',
    position: 'Project-Based Virtual Intern : UI / UX Designer',
    period: 'Jul 2023 - Aug 2023',
    emoji: '🦜',
    logo: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRxW4zjU4gLFxMQ7K2mBzwpxOHJId1nbb28LA&s',
    description: 'Project-Based Virtual Internship bersama Rakamin Academy (Nuri x Rakamin Academy).',
    responsibilities: [
      'Menyelesaikan berbagai tugas proyek yang berkaitan dengan peran UI/UX Designer di Nuri',
      'Mengerjakan solusi desain dari mulai riset hingga pembuatan User Interface dan User Experience',
      'Melakukan perancangan wireframe dasar hingga high-fidelity prototype',
    ],
    tech: ['User Experience (UX)', 'Prototyping', 'User Interface', 'Wireframing'],
    gallery: [
      { image: '/images/gallery/Nuri.png', emoji: '📱', caption: 'Final Task Nuri', description: 'Hasil proyek akhir yang difokuskan pada perancangan antarmuka pengguna untuk fitur COD di platform e-commerce Nuri.' },
      { image: '/images/gallery/6.png', emoji: '📜', caption: 'Certificate of Completion', description: 'Sertifikat kelulusan resmi dari program Virtual Internship Nuri x Rakamin Academy.' },
    ],
  },
  {
    company: 'Dinas Komunikasi dan Informatika Kab. Pekalongan',
    position: 'Student Internship',
    period: 'Sep 2021 - Oct 2021',
    emoji: '🏢',
    logo: 'https://upload.wikimedia.org/wikipedia/commons/7/74/Lambang_Kabupaten_Pekalongan.JPG',
    description: 'Menjalani masa magang dengan fokus pada desain antarmuka dan pengembangan sistem pendukung untuk wilayah lokal.',
    responsibilities: [
      'Membuat rancangan UI/UX dari aplikasi e-commerce yang ditujukan untuk memajukan UMKM di Kabupaten Pekalongan',
      'Mempelajari berbagai keterampilan (skills) baru dan langsung mengimplementasikannya pada tugas sehari-hari untuk meningkatkan efisiensi dan produktivitas',
      'Berpartisipasi aktif dalam lingkungan kerja instansi, membantu rekan tim, serta melakukan kolaborasi yang relevan dengan kebutuhan pengguna',
    ],
    tech: ['UI/UX Design', 'Figma', 'User Research', 'Prototyping'],
    gallery: [
      { image: '/images/gallery/dinkominfo.jpg', emoji: '🏢', caption: 'Gedung Dinkominfo', description: 'Gedung Dinas Komunikasi dan Informatika Kabupaten Pekalongan tempat saya melaksanakan program magang.' },
      { image: '/images/gallery/Magang.png', emoji: '🎨', caption: 'E-Commerce UMKM', description: 'Desain UI/UX (user interface & user experience) untuk platform e-commerce yang dirancang agar terjangkau dan mudah digunakan oleh pelaku UMKM.' },
    ],
  },
]

const projects = [
  {
    name: 'Fake Project',
    type: 'Landing Page',
    emoji: '🍱',
    description: 'Membuat Landing Page Website Restaurant',
    tech: ['UI/UX Design', 'Figma'],
    demo: 'https://drive.google.com/file/d/1hqhdVyanQeePJewHR8PJ9kK07BdrkfOJ/view?usp=sharing',
    github: '',
    image: '/images/portfolio/Aarss.png',
  },
  {
    name: 'Final Project Redesign Maxim',
    type: 'Redesign App',
    emoji: '🚕',
    description: 'Redesign Aplikasi Maxim dan menambahkan fitur Top Up dan Pembayaran',
    tech: ['UI/UX Design', 'Figma', 'Prototyping'],
    demo: 'https://drive.google.com/file/d/14rentR_FyblFyTi5F63m0UeVRDSomjyJ/view?usp=sharing',
    github: '',
    image: '/images/portfolio/Maxim.png',
  },
  {
    name: 'Final Task Nuri x Rakamin Academy',
    type: 'Feature Design',
    emoji: '🛍️',
    description: 'Menambahkan fitur Cash On Delivery (COD) pada aplikasi e-commerce',
    tech: ['UI/UX Design', 'Figma'],
    demo: 'https://drive.google.com/file/d/1GoF12FssWWEjVzu2kExP58ZMcDjMV4zG/view?usp=sharing',
    github: '',
    image: '/images/portfolio/Nuri.png',
  },
  {
    name: 'Final Task Niagahoster x Rakamin Academy',
    type: 'Web Design',
    emoji: '🌐',
    description: 'Membuat Checkout Flow pada website Niagahoster',
    tech: ['UI/UX Design', 'Figma'],
    demo: 'https://drive.google.com/file/d/1GdUdGYV2Tg1zPnZXwADqJSzOUguJFTPj/view?usp=sharing',
    github: '',
    image: '/images/portfolio/Niagahoster.png',
  },
  {
    name: 'Aplikasi Belanja UMKM Di Kajen',
    type: 'App Design',
    emoji: '🏪',
    description: 'Membuat UI Design Aplikasi Belanja untuk UMKM di Kajen, Kabupaten Pekalongan',
    tech: ['UI/UX Design', 'Figma'],
    demo: 'https://bit.ly/ProtoypeMagang',
    github: '',
    image: '/images/portfolio/Magang.png',
  },
  {
    name: 'Mini Task di Short Class @myskill.id',
    type: 'Mini Task',
    emoji: '📝',
    description: 'Mengerjakan Task yang diberikan pada saat mini task',
    tech: ['UI/UX Design', 'Figma'],
    demo: 'https://www.figma.com/proto/LsBpusfnm1lkL8gUjjGSLR/MiniTask---MySkill?page-id=0%3A1&type=design&node-id=2-541&viewport=609%2C593%2C0.36&t=Fq9mTWEDSw0SxcEg-1&scaling=scale-down&starting-point-node-id=2%3A541&mode=design',
    github: '',
    image: '/images/portfolio/Minitask.png',
  },
]
</script>

<style scoped>
/* Gallery Modal Transitions */
.gallery-modal-enter-active,
.gallery-modal-leave-active {
  transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
}

.gallery-modal-enter-from,
.gallery-modal-leave-to {
  opacity: 0;
}

.gallery-modal-enter-from .relative.z-10,
.gallery-modal-leave-to .relative.z-10 {
  transform: scale(0.9) translateY(20px);
}

.gallery-modal-enter-active .relative.z-10,
.gallery-modal-leave-active .relative.z-10 {
  transition: transform 0.4s cubic-bezier(0.16, 1, 0.3, 1);
}

/* Slide Transitions */
.slide-right-enter-active,
.slide-right-leave-active,
.slide-left-enter-active,
.slide-left-leave-active {
  transition: all 0.35s cubic-bezier(0.16, 1, 0.3, 1);
}

.slide-right-enter-from {
  opacity: 0;
  transform: translateX(60px) scale(0.95);
}

.slide-right-leave-to {
  opacity: 0;
  transform: translateX(-60px) scale(0.95);
}

.slide-left-enter-from {
  opacity: 0;
  transform: translateX(-60px) scale(0.95);
}

.slide-left-leave-to {
  opacity: 0;
  transform: translateX(60px) scale(0.95);
}

/* Slow bounce animation for emoji */
@keyframes bounce-slow {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-8px);
  }
}

.animate-bounce-slow {
  animation: bounce-slow 3s ease-in-out infinite;
}
</style>

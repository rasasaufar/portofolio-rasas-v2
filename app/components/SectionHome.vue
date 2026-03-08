<template>
  <section id="home" class="relative min-h-screen flex items-center overflow-hidden pt-20">
    <!-- Decorative Blobs -->
    <div class="absolute top-20 -left-32 w-96 h-96 bg-lavender-200/30 dark:bg-lavender-900/20 rounded-full blur-3xl animate-blob"></div>
    <div class="absolute bottom-20 -right-32 w-96 h-96 bg-pastel-200/30 dark:bg-pastel-900/20 rounded-full blur-3xl animate-blob" style="animation-delay: 2s"></div>
    <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[600px] bg-lavender-100/20 dark:bg-lavender-900/10 rounded-full blur-3xl animate-pulse-soft"></div>

    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 w-full">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
        <!-- Left: Text Content -->
        <div class="space-y-6 animate-fade-in-left" style="animation-delay: 0.2s">
          <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-lavender-100/60 dark:bg-lavender-900/40 border border-lavender-200/40 dark:border-lavender-800/40 backdrop-blur-sm">
            <span class="w-2 h-2 rounded-full bg-green-400 animate-pulse"></span>
            <span class="text-sm text-lavender-700 dark:text-lavender-300 font-medium">Available for opportunities</span>
          </div>

          <div class="space-y-3">
            <p class="text-lg text-lavender-500 dark:text-lavender-400 font-medium">Hello, I'm</p>
            <h1 class="text-4xl sm:text-5xl lg:text-6xl font-serif font-bold text-gray-900 dark:text-gray-100 leading-tight">
              Rasas Aufar
            </h1>
            <h2 class="text-2xl sm:text-3xl font-light text-gray-600 dark:text-gray-400">
              <span class="bg-gradient-to-r from-lavender-600 to-pastel-500 dark:from-lavender-400 dark:to-pastel-300 bg-clip-text text-transparent font-semibold">
                IT Implementation Professional
              </span>
            </h2>
          </div>

          <p class="text-gray-500 dark:text-gray-400 text-lg leading-relaxed max-w-lg">
            IT Implementation Professional experienced in managing and delivering technology solutions for 
            government projects, ensuring reliable system implementation, process optimization, and alignment 
            with organizational and public sector needs.
          </p>

          <div class="flex flex-wrap gap-4 pt-2">
            <a href="#portfolio" class="btn-primary" @click.prevent="scrollTo('portfolio')">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 11H5m14 0l-7 7m7-7l-7-7" />
              </svg>
              View Portfolio
            </a>
            <a href="#about" class="btn-outline" @click.prevent="scrollTo('about')">
              About Me
            </a>
          </div>

          <!-- Tech Stack Pills -->
          <div class="flex flex-wrap gap-2 pt-4">
            <span v-for="tech in techStack" :key="tech" class="px-3 py-1.5 text-xs font-medium rounded-lg bg-white/50 dark:bg-gray-800/50 border border-lavender-100/50 dark:border-lavender-800/50 text-gray-500 dark:text-gray-300 backdrop-blur-sm">
              {{ tech }}
            </span>
          </div>
        </div>

        <!-- Right: Photo -->
        <div class="flex justify-center lg:justify-end animate-fade-in-right" style="animation-delay: 0.4s">
          <div class="relative">
            <!-- Decorative rings -->
            <div class="absolute -inset-4 rounded-full border-2 border-dashed border-lavender-200/40 dark:border-lavender-800/40 animate-[spin_20s_linear_infinite]"></div>
            <div class="absolute -inset-8 rounded-full border border-lavender-100/30 dark:border-lavender-900/30 animate-[spin_30s_linear_infinite_reverse]"></div>

            <!-- Photo Container -->
            <div class="relative w-72 h-72 sm:w-80 sm:h-80 lg:w-96 lg:h-96 rounded-full overflow-hidden border-4 border-white/60 dark:border-gray-800/60 shadow-2xl shadow-lavender-200/40 dark:shadow-lavender-900/30">
              <img
                src="/images/profile.png"
                alt="Rasas - Profile Photo"
                class="w-full h-full object-cover"
              />
              <!-- Overlay gradient -->
              <div class="absolute inset-0 bg-gradient-to-t from-lavender-500/10 to-transparent"></div>
            </div>

            <!-- Floating Badge -->
            <div class="absolute -bottom-2 -right-2 glass-card px-4 py-2 animate-float">
              <div class="flex items-center gap-2">
                <span class="text-2xl">🚀</span>
                <div>
                  <p class="text-xs text-gray-500 dark:text-gray-400">Experience</p>
                  <p class="text-sm font-bold text-lavender-700 dark:text-lavender-300">1+ Years</p>
                </div>
              </div>
            </div>

            <!-- Floating Badge 2 -->
            <div class="absolute -top-2 -left-2 glass-card px-4 py-2 animate-float" style="animation-delay: 3s">
              <div class="flex items-center gap-2">
                <span class="text-2xl">💻</span>
                <div>
                  <p class="text-xs text-gray-500 dark:text-gray-400">Projects</p>
                  <p class="text-sm font-bold text-lavender-700 dark:text-lavender-300">5+</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Scroll Indicator -->
    <div class="absolute bottom-8 left-1/2 -translate-x-1/2 animate-bounce">
      <div class="w-6 h-10 rounded-full border-2 border-lavender-300 dark:border-lavender-700 flex justify-center pt-2">
        <div class="w-1.5 h-3 rounded-full bg-lavender-400 dark:bg-lavender-500 animate-pulse"></div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
const techStack = ['Linux', 'UI / UX Design', 'Technical Documentation', 'Database', 'Prototyping', 'Figma', 'Deployment']

const scrollTo = (id: string) => {
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
}
</script>

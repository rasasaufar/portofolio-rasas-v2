<template>
  <nav
    class="fixed top-0 left-0 right-0 z-50 transition-all duration-500"
    :class="scrolled ? 'bg-white/80 dark:bg-gray-900/80 backdrop-blur-xl shadow-lg shadow-lavender-100/20 dark:shadow-gray-900/50 border-b border-lavender-100/40 dark:border-gray-800/60' : 'bg-transparent'"
  >
    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-16 md:h-20">
        <!-- Logo -->
        <a href="#home" class="flex items-center gap-2 group" @click.prevent="scrollToSection('home')">
          <!-- Logo Typography -->
          <span class="text-xl tracking-tight font-extrabold bg-gradient-to-r from-lavender-600 via-indigo-500 to-pastel-500 dark:from-lavender-400 dark:via-indigo-400 dark:to-pastel-300 bg-clip-text text-transparent group-hover:opacity-80 transition-opacity duration-300">
            rasasaufar.site
          </span>
        </a>

        <!-- Desktop Nav -->
        <div class="hidden md:flex items-center gap-2">
          <div class="flex items-center gap-1">
            <a
              v-for="item in navItems"
              :key="item.id"
              :href="`#${item.id}`"
              class="px-4 py-2 rounded-xl text-sm font-medium transition-all duration-300"
              :class="activeSection === item.id
                ? 'bg-lavender-100 text-lavender-700 dark:bg-lavender-900/40 dark:text-lavender-300'
                : 'text-gray-500 dark:text-gray-400 hover:text-lavender-600 dark:hover:text-lavender-300 hover:bg-lavender-50 dark:hover:bg-gray-800'"
              @click.prevent="scrollToSection(item.id)"
            >
              {{ item.label }}
            </a>
          </div>

          <!-- Divider -->
          <div class="w-px h-6 bg-lavender-200/50 dark:bg-gray-700 mx-1"></div>

          <!-- Color Mode Toggle Mobile -->
          <client-only>
            <button
              @click="toggleColorMode"
              class="p-2 rounded-xl text-gray-500 dark:text-gray-400 hover:text-lavender-600 dark:hover:text-lavender-400 hover:bg-lavender-50 dark:hover:bg-gray-800 transition-colors"
            >
              <svg v-if="colorMode.value === 'dark'" class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
              </svg>
              <svg v-else class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
              </svg>
            </button>
          </client-only>
        </div>

        <!-- Mobile Menu Button -->
        <div class="flex items-center gap-2 md:hidden">
          <client-only>
            <button
              @click="toggleColorMode"
              class="p-2 rounded-xl text-gray-500 dark:text-gray-400 hover:text-lavender-600 dark:hover:text-lavender-400 hover:bg-lavender-50 dark:hover:bg-gray-800 transition-colors"
            >
              <svg v-if="colorMode.value === 'dark'" class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
              </svg>
              <svg v-else class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
              </svg>
            </button>
          </client-only>

          <button
            class="p-2 rounded-xl text-gray-600 dark:text-gray-300 hover:bg-lavender-50 dark:hover:bg-gray-800 transition-colors"
            @click="mobileOpen = !mobileOpen"
          >
            <svg v-if="!mobileOpen" class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            </svg>
            <svg v-else class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
      </div>
    </div>

    <!-- Mobile Menu -->
    <Transition
      enter-active-class="transition-all duration-300 ease-out"
      enter-from-class="opacity-0 -translate-y-4"
      enter-to-class="opacity-100 translate-y-0"
      leave-active-class="transition-all duration-200 ease-in"
      leave-from-class="opacity-100 translate-y-0"
      leave-to-class="opacity-0 -translate-y-4"
    >
      <div
        v-if="mobileOpen"
        class="md:hidden bg-white/90 dark:bg-gray-900/90 backdrop-blur-xl border-b border-lavender-100/40 dark:border-gray-800/60 shadow-lg shadow-lavender-100/20 dark:shadow-gray-900/50"
      >
        <div class="px-4 py-3 space-y-1">
          <a
            v-for="item in navItems"
            :key="item.id"
            :href="`#${item.id}`"
            class="block px-4 py-3 rounded-xl text-sm font-medium transition-all duration-300"
            :class="activeSection === item.id
              ? 'bg-lavender-100 text-lavender-700 dark:bg-lavender-900/40 dark:text-lavender-300'
              : 'text-gray-500 dark:text-gray-400 hover:text-lavender-600 dark:hover:text-lavender-300 hover:bg-lavender-50 dark:hover:bg-gray-800'"
            @click.prevent="scrollToSection(item.id); mobileOpen = false"
          >
            {{ item.label }}
          </a>
        </div>
      </div>
    </Transition>
  </nav>
</template>

<script setup lang="ts">
const scrolled = ref(false)
const mobileOpen = ref(false)
const activeSection = ref('home')
const colorMode = useColorMode()

const toggleColorMode = () => {
  colorMode.preference = colorMode.value === 'dark' ? 'light' : 'dark'
}

const navItems = [
  { id: 'home', label: 'Home' },
  { id: 'about', label: 'About Me' },
  { id: 'portfolio', label: 'Portfolio' },
  { id: 'certificate', label: 'Certificate' },
  { id: 'publication', label: 'Publication' },
]

const scrollToSection = (id: string) => {
  const el = document.getElementById(id)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth' })
  }
}

const handleScroll = () => {
  scrolled.value = window.scrollY > 50

  // Detect active section
  const sections = navItems.map(item => ({
    id: item.id,
    el: document.getElementById(item.id),
  }))

  for (let i = sections.length - 1; i >= 0; i--) {
    const section = sections[i]
    if (section?.el) {
      const rect = section.el.getBoundingClientRect()
      if (rect.top <= 150) {
        activeSection.value = section.id
        break
      }
    }
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

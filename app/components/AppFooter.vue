<template>
  <footer class="relative mt-24">
    <!-- Top Decorative Wave -->
    <div class="w-full">
      <svg viewBox="0 0 1440 120" fill="none" xmlns="http://www.w3.org/2000/svg" class="w-full block -mb-1">
        <path
          d="M0 60L48 54C96 48 192 36 288 42C384 48 480 72 576 78C672 84 768 72 864 60C960 48 1056 36 1152 36C1248 36 1344 48 1392 54L1440 60V120H0V60Z"
          fill="url(#footerGradient)"
          fill-opacity="0.5"
        />
        <defs>
          <linearGradient id="footerGradient" x1="0" y1="0" x2="1440" y2="0">
            <stop stop-color="#f0ebff" />
            <stop offset="0.5" stop-color="#e4d9ff" />
            <stop offset="1" stop-color="#f3e8ff" />
          </linearGradient>
        </defs>
      </svg>
    </div>

    <div class="bg-gradient-to-b from-lavender-50/50 dark:from-gray-900 to-lavender-100/30 dark:to-gray-950 pt-10 pb-8">
      <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="grid grid-cols-1 md:grid-cols-3 gap-10 mb-12">
          <!-- Brand -->
          <div class="space-y-4">
            <a href="#home" class="inline-flex items-center group cursor-pointer" @click.prevent="scrollToSection('home')">
              <span class="text-2xl tracking-tight font-extrabold bg-gradient-to-r from-lavender-600 via-indigo-500 to-pastel-500 dark:from-lavender-400 dark:via-indigo-400 dark:to-pastel-300 bg-clip-text text-transparent group-hover:opacity-80 transition-opacity duration-300">
                rasasaufar.site
              </span>
            </a>
            <p class="text-gray-500 dark:text-gray-400 text-sm leading-relaxed">
              IT Implementation Professional passionate about creating impactful digital solutions and sharing knowledge through publications.
            </p>
          </div>

          <!-- Quick Links -->
          <div>
            <h4 class="text-sm font-semibold text-gray-800 dark:text-gray-200 uppercase tracking-wider mb-4">Quick Links</h4>
            <ul class="space-y-3">
              <li v-for="item in quickLinks" :key="item.id">
                <a
                  :href="`#${item.id}`"
                  class="text-gray-500 dark:text-gray-400 hover:text-lavender-600 dark:hover:text-lavender-400 text-sm transition-colors duration-300 flex items-center gap-2 group cursor-pointer"
                  @click.prevent="scrollToSection(item.id)"
                >
                  <span class="w-1.5 h-1.5 rounded-full bg-lavender-300 dark:bg-lavender-700 group-hover:bg-lavender-500 dark:group-hover:bg-lavender-500 transition-colors duration-300 flex-shrink-0"></span>
                  {{ item.label }}
                </a>
              </li>
            </ul>
          </div>

          <!-- Contact -->
          <div>
            <h4 class="text-sm font-semibold text-gray-800 dark:text-gray-200 uppercase tracking-wider mb-4">Connect</h4>
            <div class="flex gap-3">
              <a
                v-for="social in socials"
                :key="social.name"
                :href="social.url"
                target="_blank"
                rel="noopener noreferrer"
                class="w-10 h-10 rounded-xl bg-white/60 dark:bg-gray-800/60 border border-lavender-100 dark:border-gray-700/50 flex items-center justify-center text-gray-400 dark:text-gray-500 hover:text-lavender-600 dark:hover:text-lavender-400 hover:bg-lavender-50 dark:hover:bg-gray-800 hover:border-lavender-200 dark:hover:border-lavender-900/50 hover:-translate-y-1 transition-all duration-300 shadow-sm cursor-pointer"
                :title="social.name"
              >
                <!-- WhatsApp -->
                <svg v-if="social.name === 'WhatsApp'" class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                  <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51a12.8 12.8 0 0 0-.57-.01c-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 0 1-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 0 1-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 0 1 2.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0 0 12.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 0 0 5.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 0 0-3.48-8.413z"/>
                </svg>
                <!-- Email -->
                <svg v-else-if="social.name === 'Email'" class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                </svg>
                <!-- LinkedIn -->
                <svg v-else-if="social.name === 'LinkedIn'" class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                  <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
                </svg>
                <!-- Instagram -->
                <svg v-else-if="social.name === 'Instagram'" class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                  <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 100 12.324 6.162 6.162 0 000-12.324zM12 16a4 4 0 110-8 4 4 0 010 8zm6.406-11.845a1.44 1.44 0 100 2.881 1.44 1.44 0 000-2.881z"/>
                </svg>
              </a>
            </div>
          </div>
        </div>

        <!-- Bottom Bar -->
        <div class="border-t border-lavender-200/50 dark:border-gray-800 pt-6 flex flex-col md:flex-row items-center justify-between gap-4">
          <p class="text-xs text-gray-400 dark:text-gray-500">
            &copy; {{ new Date().getFullYear() }} Rasas Aufar. All rights reserved.
          </p>
          <p class="text-xs text-gray-400 dark:text-gray-500">
            Built with <span class="text-lavender-400 dark:text-lavender-500">♥</span> using Nuxt & TailwindCSS
          </p>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
const quickLinks = [
  { id: 'home', label: 'Home' },
  { id: 'about', label: 'About Me' },
  { id: 'portfolio', label: 'Portfolio' },
  { id: 'certificate', label: 'Certificate' },
  { id: 'publication', label: 'Publication' },
]

const socials = [
  { name: 'WhatsApp', url: 'https://wa.me/085326775595' },
  { name: 'Email', url: 'mailto:rasasaufar4@gmail.com' },
  { name: 'LinkedIn', url: 'https://www.linkedin.com/in/rasas-aufar/' },
  { name: 'Instagram', url: 'https://instagram.com/rasasaufar' },
]

const scrollToSection = (id: string) => {
  const el = document.getElementById(id)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>

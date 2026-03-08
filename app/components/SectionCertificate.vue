<template>
  <section id="certificate" class="py-24 relative">
    <!-- Decorative background -->
    <div class="absolute top-0 right-0 w-96 h-96 bg-lavender-100/20 dark:bg-lavender-900/10 rounded-full blur-3xl -translate-y-1/2"></div>

    <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 relative">
      <!-- Section Header -->
      <div class="text-center mb-16 animate-on-scroll">
        <span class="badge mb-4">Certificates</span>
        <h2 class="section-title">Achievements and Certifications</h2>
        <p class="section-subtitle">Professional certifications and accomplishments I've earned</p>
      </div>

      <!-- Certificates Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <div
          v-for="(cert, index) in certificates"
          :key="cert.name"
          class="glass-card-solid overflow-hidden card-hover animate-on-scroll group"
          :style="{ animationDelay: `${index * 0.1}s` }"
        >
          <!-- Certificate Visual -->
          <!-- Certificate Visual -->
          <div class="relative h-44 overflow-hidden bg-white dark:bg-[#f8f9fa] border-b border-gray-100/80 dark:border-gray-200">
            <!-- Decorative Pattern (Grid & Soft Blobs) -->
            <div class="absolute inset-0 z-0 opacity-60 pointer-events-none">
              <div class="absolute inset-0 bg-[linear-gradient(to_right,#80808012_1px,transparent_1px),linear-gradient(to_bottom,#80808012_1px,transparent_1px)] bg-[size:20px_20px]"></div>
            </div>
            <!-- Soft Glowing Orbs -->
            <div class="absolute -top-12 -right-12 w-48 h-48 bg-lavender-100/80 dark:bg-lavender-200/60 rounded-full blur-3xl z-0 pointer-events-none"></div>
            <div class="absolute -bottom-12 -left-12 w-48 h-48 bg-blue-50/90 dark:bg-blue-200/50 rounded-full blur-3xl z-0 pointer-events-none"></div>

            <!-- Certificate Icon / Logo -->
            <div class="absolute inset-0 z-10 flex items-center justify-center pointer-events-none">
              <div 
                class="flex items-center justify-center group-hover:scale-110 group-hover:-rotate-3 transition-transform duration-500 relative" 
                :class="cert.image ? 'w-28 h-28 drop-shadow-xl' : 'w-16 h-16 rounded-2xl bg-white border border-gray-200/80 shadow-md overflow-hidden'"
              >
                <img v-if="cert.image" :src="cert.image" :alt="cert.name" class="w-full h-full object-contain" />
                <span v-else class="text-3xl drop-shadow-sm">{{ cert.emoji }}</span>
              </div>
            </div>

            <!-- Issue Date Badge -->
            <div class="absolute top-4 right-4 z-20 flex items-center gap-1.5 px-3 py-1.5 rounded-full bg-white/80 hover:bg-white backdrop-blur-md border border-gray-200/80 shadow-sm transition-all duration-300 group/badge">
              <svg class="w-3.5 h-3.5 text-lavender-600 group-hover/badge:scale-110 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
              </svg>
              <span class="text-xs font-semibold text-slate-700 tracking-wide">{{ cert.year }}</span>
            </div>
          </div>

          <!-- Certificate Info -->
          <div class="p-6 space-y-3">
            <h3 class="font-bold text-gray-800 dark:text-gray-100 group-hover:text-lavender-700 dark:group-hover:text-lavender-400 transition-colors duration-300">
              {{ cert.name }}
            </h3>
            <p class="text-sm text-lavender-600 dark:text-lavender-400 font-medium flex items-center gap-1.5">
              <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4" />
              </svg>
              {{ cert.issuer }}
            </p>
            <p class="text-xs text-gray-400 dark:text-gray-500 leading-relaxed">{{ cert.description }}</p>

            <!-- Score Highlight -->
            <div v-if="cert.score" class="inline-flex mt-1">
              <div class="px-2.5 py-1 rounded-lg bg-gradient-to-r from-amber-100 to-orange-100 dark:from-amber-900/40 dark:to-orange-900/40 border border-amber-200/50 dark:border-amber-700/50 flex items-center gap-1.5 shadow-sm transform hover:scale-105 transition-transform">
                <svg class="w-3.5 h-3.5 text-amber-600 dark:text-amber-400" fill="currentColor" viewBox="0 0 20 20">
                  <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
                </svg>
                <span class="text-xs font-bold text-amber-800 dark:text-amber-300">Score: {{ cert.score }}</span>
              </div>
            </div>

            <!-- Skills Tags -->
            <div v-if="cert.skills && cert.skills.length > 0" class="flex flex-wrap gap-1.5">
              <span v-for="skill in cert.skills" :key="skill" class="px-2 py-0.5 text-xs rounded-md bg-lavender-50 dark:bg-lavender-900/30 text-lavender-600 dark:text-lavender-300 border border-lavender-100/40 dark:border-lavender-800/40">
                {{ skill }}
              </span>
            </div>

            <div class="pt-3 mt-1 border-t border-lavender-100/40 dark:border-gray-700/50 flex items-center justify-between gap-2">
              <div v-if="cert.id" class="flex items-center gap-1.5 min-w-0 font-mono" title="Credential ID">
                <svg class="w-3.5 h-3.5 text-lavender-400 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4" />
                </svg>
                <span class="text-[11px] text-gray-400 truncate">{{ cert.id }}</span>
              </div>
              <div v-else></div>
              <span
                class="inline-flex items-center gap-1 px-2.5 py-1 text-[10px] rounded-full font-semibold uppercase tracking-wider flex-shrink-0"
                :class="cert.verified ? 'bg-green-50 dark:bg-green-900/20 text-green-700 dark:text-green-400 border border-green-100 dark:border-green-800/50' : 'bg-gray-50 dark:bg-gray-800 text-gray-500 dark:text-gray-400 border border-gray-100 dark:border-gray-700'"
              >
                <svg v-if="cert.verified" class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
                </svg>
                {{ cert.verified ? 'Verified' : 'Completed' }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
const certificates = [
  {
    name: 'Wawasan Karir dalam Bidang Data Analytics',
    issuer: 'Digital Talent Scholarship',
    year: 'Jul 2025',
    image: '/images/certificates/dts-logo.png',
    emoji: '📊',
    description: 'Pelatihan wawasan karir di bidang Data Analytics melalui program Digital Talent Scholarship.',
    id: '2299746850-4500',
    skills: ['Data Analytics', 'Data Visualization'],
    bgGradient: 'bg-gradient-to-br from-sky-400 to-blue-500',
    verified: true,
  },
  {
    name: 'Pengenalan Data Science dan Pemanfaatannya dalam Berbagai Sektor',
    issuer: 'Digital Talent Scholarship',
    year: 'Jul 2025',
    image: '/images/certificates/dts-logo.png',
    emoji: '🔬',
    description: 'Pelatihan pengenalan Data Science dan penerapannya di berbagai sektor industri melalui Digital Talent Scholarship.',
    id: '2299818850-4751',
    skills: ['Data Science', 'Data Analysis'],
    bgGradient: 'bg-gradient-to-br from-fuchsia-400 to-purple-500',
    verified: true,
  },
  {
    name: 'Keamanan IT: Pertahanan terhadap Kejahatan Digital',
    issuer: 'Coursera',
    year: 'Jul 2024',
    image: '/images/certificates/coursera-logo.png',
    emoji: '🔒',
    description: 'Kursus keamanan IT dari Google IT Support Specialization.',
    id: 'TDN7P3MAAEG7',
    skills: ['Cybersecurity', 'Encryption', 'Network Security'],
    bgGradient: 'bg-gradient-to-br from-red-400 to-rose-500',
    verified: true,
  },
  {
    name: 'Administrasi Sistem dan Layanan Infrastruktur TI',
    issuer: 'Coursera',
    year: 'Jul 2024',
    image: '/images/certificates/coursera-logo.png',
    emoji: '🖥️',
    description: 'Kursus administrasi sistem dari Google IT Support Specialization.',
    id: 'RC8NK9PBR5XG',
    skills: ['Server Management', 'Directory Services', 'IT Infrastructure'],
    bgGradient: 'bg-gradient-to-br from-indigo-400 to-purple-500',
    verified: true,
  },
  {
    name: 'Sistem Operasi dan Anda: Menjadi Pengguna yang Berdaya',
    issuer: 'Coursera',
    year: 'Jul 2024',
    image: '/images/certificates/coursera-logo.png',
    emoji: '💻',
    description: 'Kursus tentang sistem operasi dari Google IT Support Specialization.',
    id: '7KU8JRMPQVHJ',
    skills: ['Windows', 'Linux', 'File Management', 'Command Line'],
    bgGradient: 'bg-gradient-to-br from-violet-400 to-purple-600',
    verified: true,
  },
  {
    name: 'Spesialisasi IT Support Google',
    issuer: 'Google',
    year: 'Jul 2024',
    image: '/images/certificates/google-logo.png',
    emoji: '🔧',
    description: 'Sertifikasi profesional dari Google yang mencakup berbagai keahlian IT.',
    id: 'YL552W7AGU2G',
    skills: ['Cloud Computing', 'Computer Networking', 'IT Security', 'System Administration', 'Troubleshooting', 'Operating Systems'],
    bgGradient: 'bg-gradient-to-br from-blue-400 to-cyan-500',
    verified: true,
  },
  {
    name: 'Seluk Beluk Jaringan Komputer',
    issuer: 'Coursera',
    year: 'Jun 2024',
    image: '/images/certificates/coursera-logo.png',
    emoji: '🌐',
    description: 'Kursus jaringan komputer dari Google IT Support Specialization.',
    id: '2FLPLT9K6MXS',
    skills: ['TCP/IP', 'DNS', 'DHCP', 'Network Troubleshooting'],
    bgGradient: 'bg-gradient-to-br from-teal-400 to-cyan-500',
    verified: true,
  },
  {
    name: 'Dasar-Dasar Dukungan Teknis',
    issuer: 'Coursera',
    year: 'Mei 2024',
    image: '/images/certificates/coursera-logo.png',
    emoji: '🛠️',
    description: 'Kursus dasar dukungan teknis dari Google IT Support Specialization.',
    id: '7C2ZULPDA5P6',
    skills: ['Troubleshooting', 'Customer Service', 'Operating Systems'],
    bgGradient: 'bg-gradient-to-br from-blue-500 to-indigo-600',
    verified: true,
  },
  {
    name: 'TOEFL',
    issuer: 'Englishvit',
    year: 'Okt 2023',
    image: '/images/certificates/englishvit-logo.png',
    emoji: '📝',
    description: 'Sertifikat kemampuan bahasa Inggris melalui tes TOEFL online. Berlaku hingga Oktober 2025.',
    score: '542',
    id: 'EV/TO4/10/2023/0159',
    skills: ['English Proficiency', 'TOEFL'],
    bgGradient: 'bg-gradient-to-br from-emerald-400 to-green-500',
    verified: true,
  },
  {
    name: 'Certificate of Mastery UI-UX Research and Design: Fullstack Intensive Bootcamp',
    issuer: 'MySkill',
    year: 'Sep 2023',
    image: '/images/certificates/myskill-logo.png',
    emoji: '🏅',
    description: 'Sertifikat kelulusan bootcamp intensif UI-UX Research and Design Fullstack.',
    id: 'MS-1/9/2023-5qlzkE6XeBcbQREEVF0I',
    skills: ['User Interface', 'User Experience (UX)', 'Design Research'],
    bgGradient: 'bg-gradient-to-br from-amber-500 to-orange-600',
    verified: true,
  },
  {
    name: 'Certificate of Competencies - Nuri UI/UX Designer Virtual Internship',
    issuer: 'Nuri',
    year: 'Jul 2023',
    image: '/images/certificates/nuri-logo.png',
    emoji: '🦜',
    description: 'Sertifikat kompetensi UI/UX Designer melalui program virtual internship Nuri x Rakamin Academy.',
    id: '212536IAPMGIN2672023',
    skills: ['Sketching', 'Design Thinking', 'User Interface', 'User Experience', 'Prototyping'],
    bgGradient: 'bg-gradient-to-br from-green-400 to-emerald-500',
    verified: true,
  },
  {
    name: 'Figma For UI/UX Design',
    issuer: 'MySkill',
    year: 'Jul 2023',
    image: '/images/certificates/myskill-logo.png',
    emoji: '🖌️',
    description: 'Pelatihan desain UI/UX menggunakan Figma.',
    id: '48508/UIX/LM/07/2023',
    skills: ['Figma', 'User Interface Design'],
    bgGradient: 'bg-gradient-to-br from-purple-400 to-pink-500',
    verified: true,
  },
  {
    name: 'Fundamental UX Design',
    issuer: 'Coding Studio',
    year: 'Jul 2023',
    image: '/images/certificates/coding-studio-logo.png',
    emoji: '🧩',
    description: 'Pelatihan dasar User Experience Design.',
    id: '77DF6D121A-77F17BB889-75BB1E65BD',
    skills: ['User Experience (UX)', 'UX Research', 'UX Writing'],
    bgGradient: 'bg-gradient-to-br from-cyan-400 to-blue-500',
    verified: true,
  },
  {
    name: 'Fundamental UI Design',
    issuer: 'Coding Studio',
    year: 'Jul 2023',
    image: '/images/certificates/coding-studio-logo.png',
    emoji: '🎯',
    description: 'Pelatihan dasar User Interface Design.',
    id: '77DF6D121A-75C17F8C7B-75BB1E65BD',
    skills: ['User Interface Design', 'Visual Design', 'Layout'],
    bgGradient: 'bg-gradient-to-br from-pink-400 to-rose-500',
    verified: true,
  },
  {
    name: 'Certificate of Competencies - Niagahoster UI/UX Designer Virtual Internship',
    issuer: 'Niagahoster - Web Hosting Unlimited Indonesia',
    year: 'Jul 2023',
    image: '/images/certificates/niagahoster-logo.png',
    emoji: '🎨',
    description: 'Sertifikat kompetensi UI/UX Designer melalui program virtual internship Niagahoster x Rakamin Academy.',
    id: '212536IAPMGIN3072023',
    skills: ['User Journeys', 'Process Design', 'UI Design', 'UX Research', 'Wireframing', 'Prototyping'],
    bgGradient: 'bg-gradient-to-br from-blue-500 to-indigo-500',
    verified: true,
  },
  {
    name: 'AWS Certified Cloud Practitioner',
    issuer: 'Amazon Web Services (AWS)',
    year: 'Mei 2023',
    image: '/images/certificates/aws-cloud-practitioner.png',
    emoji: '☁️',
    description: 'Sertifikasi resmi AWS yang memvalidasi pemahaman dasar tentang layanan AWS Cloud, arsitektur, dan best practices. Berlaku hingga Mei 2026.',
    skills: ['Cloud Computing', 'AWS Services', 'Cloud Architecture', 'Security'],
    bgGradient: 'bg-gradient-to-br from-orange-400 to-yellow-500',
    verified: true,
  },
  {
    name: 'AWS Cloud Foundation',
    issuer: 'Digital Talent Scholarship',
    year: 'Mei 2023',
    image: '/images/certificates/dts-logo.png',
    emoji: '☁️',
    description: 'Sertifikat pelatihan melalui program beasiswa Digital Talent Scholarship oleh Kominfo.',
    id: '1955634840-1099/FGA/BLSDM.Kominfo/2023',
    skills: ['Cloud Computing'],
    bgGradient: 'bg-gradient-to-br from-amber-400 to-orange-500',
    verified: true,
  },
  {
    name: 'AWS Academy Graduate - AWS Academy Cloud Foundations',
    issuer: 'Amazon Web Services (AWS)',
    year: 'Mar 2023',
    image: '/images/certificates/aws-cloud-security.png',
    emoji: '🎓',
    description: 'Kelulusan program AWS Academy Cloud Foundations yang mencakup konsep dasar cloud, layanan inti AWS, keamanan, dan arsitektur.',
    skills: ['Cloud Foundations', 'AWS Core Services', 'Cloud Security'],
    bgGradient: 'bg-gradient-to-br from-yellow-400 to-amber-500',
    verified: true,
  },
  {
    name: 'Certificate Of Competence Junior Web Developer',
    issuer: 'Badan Nasional Sertifikasi Profesi (BNSP)',
    year: 'Agu 2022',
    image: '/images/certificates/bnsp-logo.png',
    emoji: '🏆',
    description: 'Sertifikasi kompetensi nasional sebagai Junior Web Developer dari BNSP. Berlaku hingga Agustus 2025.',
    id: '62019 2513 18247 2022',
    skills: ['CSS', 'HTML', 'Web Development'],
    bgGradient: 'bg-gradient-to-br from-red-500 to-orange-500',
    verified: true,
  },
]
</script>

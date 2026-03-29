<template>
  <div class="min-h-screen bg-[#f5ede3] flex flex-col">

    <!-- ── Top bar ── -->
    <header class="bg-[#f5ede3] border-b border-[#e8ddd0] px-6 py-3 flex items-center justify-between">
      <NuxtLink to="/" class="flex items-center gap-2 no-underline">
        <img src="@/assets/images/logo/logo.png" alt="Credeny" class="w-100 h-12" />
      </NuxtLink>
      <NuxtLink
        to="/login"
        class="text-sm font-bold text-white bg-[#1a1a2e] hover:bg-[#2d2d4e] px-5 py-2 rounded-lg transition-all duration-200 hover:-translate-y-px"
      >
        Login
      </NuxtLink>
    </header>

    <!-- ── Main content ── -->
    <main class="flex-1  mx-auto w-full px-6 py-12">

      <!-- Org logo -->
      <div class="flex justify-center mb-5">
        <img
          :src="org.logo"
          :alt="org.name"
          class="w-100 h-100 rounded-full object-cover border-4 border-white shadow-md"
        />
      </div>

      <!-- Issuer avatars (small overlapping) -->
      <div class="flex justify-center mb-4">
        <div class="flex items-center">
          <div
            v-for="(issuer, i) in org.issuers"
            :key="i"
            class="w-9 h-9 rounded-full border-2 border-[#f5ede3] overflow-hidden flex-shrink-0"
            :class="i > 0 ? '-ml-2' : ''"
            :style="`z-index: ${org.issuers.length - i}`"
          >
            <img
              v-if="issuer.avatar"
              :src="issuer.avatar"
              :alt="issuer.name"
              class="w-full h-full object-cover"
            />
            <div
              v-else
              class="w-full h-full flex items-center justify-center text-xs font-bold text-white"
              :style="`background-color: ${issuer.color}`"
            >
              {{ issuer.initials }}
            </div>
          </div>
        </div>
      </div>

      <!-- Org name -->
      <h1 class="text-xl font-extrabold text-[#1a1a2e] text-center mb-4 tracking-tight">
        {{ org.name }}
      </h1>

      <!-- Description -->
      <p class="text-[#555] text-center leading-relaxed w-[80%] mx-auto mb-8 ">
        {{ org.description }}
      </p>

      <!-- Contact address -->
      <div class="flex items-center justify-center mb-10">
        <div class="flex items-center gap-4 bg-white border border-dashed border-[#e8ddd0] rounded-xl px-6 py-5 shadow-lg">
          <span class="font-bold text-lg text-[#1a1a2e] whitespace-nowrap">Contact Address :</span>
          <span class="text-lg text-[#555]">{{ org.contactEmail }}</span>
        </div>
      </div>

      <!-- Badges banner -->
      <div class="relative w-[80%] mx-auto rounded-2xl overflow-hidden mb-10 h-[250px] flex items-center justify-center">
        <img
          src="@/assets/images/backgrounds/dashboard-banner.png"
          alt=""
          class="absolute inset-0 w-full h-full object-cover"
        />
        <div class="absolute inset-0 bg-black/15"></div>
        <div class="relative z-10 text-center">
          <h2 class="text-4xl font-extrabold text-[#1a1a2e] tracking-tight">Badges</h2>
          <p class="text-[#333] mt-1">All badges Created by this organization</p>
        </div>
      </div>

      <!-- Badges grid -->
      <div class="bg-white rounded-2xl mt-8 w-[80%] mx-auto border-dashed border border-[#f0e6d8] p-20">
        <div class="grid grid-cols-2 sm:grid-cols-4 gap-10">
          <NuxtLink
            v-for="badge in badges"
            :key="badge.id"
            :to="`/badge/${badge.id}`"
            class="rounded-2xl px-3 py-5 border bg-[#FFF7EE] border-[#f0e6d8] hover:shadow-md hover:-translate-y-0.5 transition-all duration-200 cursor-pointer group block"
          >
            <!-- Badge image -->
            <div class="flex justify-center mb-3 ">
              <img
                :src="badge.image"
                :alt="badge.title"
                class=" rounded-full object-cover border-4 border-[#f5ede3]  group-hover:border-[#c8873a] transition-colors duration-200"
              />
            </div>
            <!-- Info -->
            <div class="flex items-start justify-between gap-1">
              <div class="min-w-0">
                <h3 class="font-bold text-xs text-[#1a1a2e] truncate">{{ badge.title }}</h3>
                <p class="text-[11px] text-[#888] leading-relaxed mt-0.5 line-clamp-2">{{ badge.description }}</p>
                <p class="text-[10px] text-[#aaa] mt-1.5">{{ badge.date }}</p>
              </div>
              <button
                class="flex-shrink-0 p-0.5 rounded hover:bg-[#f0e6d8] transition-colors duration-200 mt-0.5"
                @click.prevent="openMenu(badge.id)"
              >
                <svg class="w-3.5 h-3.5 text-[#aaa]" fill="currentColor" viewBox="0 0 24 24">
                  <path d="M12 13a1 1 0 110-2 1 1 0 010 2zm0-5a1 1 0 110-2 1 1 0 010 2zm0 10a1 1 0 110-2 1 1 0 010 2z"/>
                </svg>
              </button>
            </div>
          </NuxtLink>
        </div>
      </div>

    </main>

    <!-- ── Footer ── -->
    <footer class="bg-[#1a1a2e] py-6 px-6 mt-auto">
      <div class="max-w-[720px] mx-auto flex flex-col items-center gap-3">
        <div class="flex items-center gap-6">
          <NuxtLink to="/privacy" class="text-sm text-white/60 hover:text-white transition-colors duration-200">
            Privacy Policy
          </NuxtLink>
          <NuxtLink to="/terms" class="text-sm text-white/60 hover:text-white transition-colors duration-200">
            Terms Of Use
          </NuxtLink>
        </div>
        <p class="text-xs text-white/35">
          (C) {{ year }}  Powered by Credeny
        </p>
      </div>
    </footer>

  </div>
</template>

<script setup>
import companyLogo from '@/assets/images/logo/company-logo.png'
definePageMeta({ layout: false })

const year = new Date().getFullYear()

// to be replaced using route.params.id
// const route = useRoute()
// const { data: org } = await useFetch(`/api/organizations/${route.params.id}`)

const org = ref({
  name: 'Major Corporation',
  logo: companyLogo,
  description: 'Potter ipsum wand elf parchment wingardium. In yer locomotor glasses holyhead good glory points. Kedavra prophet headmaster broomstick charm. Knut bezoar leviosa yer gillwater portrait bat it good frisbees. Turban veela and yer crookshanks. Firs\' eye splinched order great mellows cake. Grindlewald die tap-dancing owl plums cakes. Together sinistra he mischief stand mcgonagall witch. Hsorcerer\'s patronus gamp\'s sopophorous patronum feast fanged. Scabbers gillywater glass owl jinxes roaring. He doe other sorcerer\'s thieves clean law.',
  contactEmail: 'MajorCorps@gmail.com',

})

const badges = ref([
  { id: 1, title: 'Design Degree I', description: 'Certificate of Completion in design and Visual Asset Production', date: '4th april 2024', image: '/images/randoms/badge.png' },
  { id: 2, title: 'Design Degree I', description: 'Certificate of Completion in design and Visual Asset Production', date: '4th april 2024', image: '/images/randoms/badge.png' },
  { id: 3, title: 'Design Degree I', description: 'Certificate of Completion in design and Visual Asset Production', date: '4th april 2024', image: '/images/randoms/badge.png' },
  { id: 4, title: 'Design Degree I', description: 'Certificate of Completion in design and Visual Asset Production', date: '4th april 2024', image: '/images/randoms/badge.png' },
  { id: 5, title: 'Design Degree I', description: 'Certificate of Completion in design and Visual Asset Production', date: '4th april 2024', image: '/images/randoms/badge.png' },
  { id: 6, title: 'Design Degree I', description: 'Certificate of Completion in design and Visual Asset Production', date: '4th april 2024', image: '/images/randoms/badge.png' },
  { id: 7, title: 'Design Degree I', description: 'Certificate of Completion in design and Visual Asset Production', date: '4th april 2024', image: '/images/randoms/badge.png' },
  { id: 8, title: 'Design Degree I', description: 'Certificate of Completion in design and Visual Asset Production', date: '4th april 2024', image: '/images/randoms/badge.png' },
])

const openMenu = (id) => {
  console.log('Open menu for badge:', id)
}

useHead({ title: `${org.value.name} — Credeny` })
</script>
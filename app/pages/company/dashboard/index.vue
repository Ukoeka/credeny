<template>
  <div>

    <!-- ── Hero Banner ── -->
    <div class="relative w-full rounded-2xl overflow-hidden mb-8 h-[250px] flex items-center justify-center">
      <img
        src="@/assets/images/backgrounds/dashboard-banner.png"
        alt=""
        class="absolute inset-0 w-full h-full object-cover"
      />
      <div class="absolute inset-0 bg-black/20"></div>

      <!-- Create Badge button top-right -->
      <NuxtLink
        to="/issuer/dashboard/badges/create"
        class="absolute top-4 right-4 z-20 flex items-center gap-2 text-xs font-semibold text-[#1a1a2e] bg-white/90 hover:bg-white px-3 py-2 rounded-lg shadow transition-all duration-200 backdrop-blur-sm"
      >
        Create Badge
        <div class="w-5 h-5 rounded-full bg-[#1a1a2e] flex items-center justify-center flex-shrink-0">
          <svg class="w-3 h-3 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="3">
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 4v16m8-8H4"/>
          </svg>
        </div>
      </NuxtLink>

      <div class="relative z-10 text-center">
        <h1 class="text-4xl lg:text-5xl font-extrabold text-[#1a1a2e] tracking-tight">Badges</h1>
        <p class="text-[#333] text-lg mt-1">All badges you have created</p>
      </div>
    </div>

    <!-- ── EMPTY STATE ── -->
    <div v-if="badges.length === 0" class="flex flex-col items-center justify-center px-20 py-24">
      <img
        src="@/assets/images/randoms/web.png"
        alt="No badges"
        class="w-full h-full object-contain opacity-60 mb-6"
      />
      <p class="text-lg font-semibold text-[#c8b89a]">No Badges Yet</p>
      <NuxtLink
        to="/issuer/dashboard/badges/create"
        class="mt-6 inline-block text-sm font-bold text-white bg-[#1a1a2e] hover:bg-[#2d2d4e] px-6 py-3 rounded-xl transition-all duration-200 hover:-translate-y-px"
      >
        Create your first Badge
      </NuxtLink>
    </div>

    <!-- ── POPULATED STATE ── -->
    <div v-else class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-10">
      <NuxtLink
        v-for="badge in badges"
        :key="badge.id"
        class="bg-white rounded-2xl p-4 border border-[#f0e6d8] hover:shadow-md hover:-translate-y-0.5 transition-all duration-200 cursor-pointer group block"
        :to="`/issuer/dashboard/badges/${badge.id}`"
      >
        <!-- Badge image -->
        <div class="flex justify-center mb-3">
          <img
            :src="badge.image"
            :alt="badge.title"
            class="w-full rounded-full object-cover border-4 border-[#f5ede3] group-hover:border-[#c8873a] transition-colors duration-200"
          />
        </div>

        <!-- Info -->
        <div class="flex items-start justify-between gap-1">
          <div class="min-w-0">
            <h3 class="font-bold text-sm text-[#1a1a2e] truncate">{{ badge.title }}</h3>
            <p class="text-xs text-[#888] leading-relaxed mt-0.5 line-clamp-2">{{ badge.description }}</p>
            <p class="text-xs text-[#aaa] mt-2">{{ badge.date }}</p>
          </div>
          <!-- More options -->
          <button
            class="flex-shrink-0 p-1 rounded-md hover:bg-[#f0e6d8] transition-colors duration-200 mt-0.5"
            @click.prevent="openMenu(badge.id)"
          >
            <svg class="w-4 h-4 text-[#aaa]" fill="currentColor" viewBox="0 0 24 24">
              <path d="M12 13a1 1 0 110-2 1 1 0 010 2zm0-5a1 1 0 110-2 1 1 0 010 2zm0 10a1 1 0 110-2 1 1 0 010 2z"/>
            </svg>
          </button>
        </div>
      </NuxtLink>
    </div>

  </div>
</template>

<script setup>
definePageMeta({ layout: 'companydashboard' })

// Replace with real API data
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

useHead({ title: 'Badges — Credeny Issuer' })
</script>
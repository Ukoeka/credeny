<template>
  <div>
    <div class="relative w-full rounded-2xl overflow-hidden P-12 mb-8 h-[250px] flex items-center justify-center">
      <img
        src="@/assets/images/backgrounds/dashboard-banner.png"
        alt=""
        class="absolute inset-0 w-full h-full object-cover"
      />
      <div class="absolute inset-0 bg-black/20"></div>
      <div class="relative z-10 text-center">
        <h1 class="text-2xl lg:text-3xl font-extrabold text-[#1a1a2e] tracking-tight">Display Shelf</h1>
        <p class="text-sm text-[#333] mt-1">All your badges and achievements in one place</p>
      </div>
    </div>

    <!-- ── EMPTY STATE ── -->
    <div v-if="badges.length === 0" class="flex flex-col items-center justify-center px-20 py-24">
      <img
        src="@/assets/images/randoms/web.png"
        alt="Empty shelf"
        class="w-full h-full object-contain opacity-60 mb-6"
      />
      <p class="text-lg font-semibold text-[#c8b89a]">Shelf so Empty</p>
    </div>

    <!-- ── POPULATED STATE ── -->
    <div v-else class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-10">
      <div
        v-for="badge in badges"
        :key="badge.id"
        class="bg-white rounded-2xl p-10 border border-[#f0e6d8] hover:shadow-md hover:-translate-y-0.5 transition-all duration-200 cursor-pointer group"
        @click="navigateTo(`/dashboard/badge/${badge.id}`)"
      >
        <!-- Badge image -->
        <div class="flex justify-center mb-3">
          <img
            :src="badge.image"
            :alt="badge.title"
            class="w-full h-auto rounded-full object-cover border-4 border-[#f5ede3] group-hover:border-[#c8873a] transition-colors duration-200"
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
            @click.stop="openMenu(badge.id)"
          >
            <svg class="w-4 h-4 text-[#aaa]" fill="currentColor" viewBox="0 0 24 24">
              <path d="M12 13a1 1 0 110-2 1 1 0 010 2zm0-5a1 1 0 110-2 1 1 0 010 2zm0 10a1 1 0 110-2 1 1 0 010 2z"/>
            </svg>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({ layout: 'dashboard' })

// Replace with real API data
const badges = ref([
  {
    id: 1,
    title: 'Design Degree I',
    description: 'Certificate of Completion in design and Visual Asset Production',
    date: '4th April 2024',
    image: '/images/randoms/badge.png',
  },
  {
    id: 2,
    title: 'Design Degree II',
    description: 'Certificate of Completion in design and Visual Asset Production',
    date: '4th April 2024',
    image: '/images/randoms/badge.png',
  },
  {
    id: 3,
    title: 'Design Degree I',
    description: 'Certificate of Completion in design and Visual Asset Production',
    date: '4th April 2024',
    image: '/images/randoms/badge.png',
  },
  {
    id: 4,
    title: 'Design Degree I',
    description: 'Certificate of Completion in design and Visual Asset Production',
    date: '4th April 2024',
    image: '/images/randoms/badge.png',
  },
  {
    id: 5,
    title: 'Recycle Course',
    description: 'Certificate of completion Issued By Max Foundation',
    date: '4th April 2024',
    image: '/images/randoms/badge.png',
  },
  {
    id: 6,
    title: 'Design Degree I',
    description: 'Certificate of Completion in design and Visual Asset Production',
    date: '4th April 2024',
    image: '/images/randoms/badge.png',
  },
  {
    id: 7,
    title: 'Design Degree I',
    description: 'Certificate of Completion in design and Visual Asset Production',
    date: '4th April 2024',
    image: '/images/randoms/badge.png',
  },
  {
    id: 8,
    title: 'Design Degree I',
    description: 'Certificate of Completion in design and Visual Asset Production',
    date: '4th April 2024',
    image: '/images/randoms/badge.png',
  },
])

const openMenu = (id) => {
  // Handle badge options menu
  console.log('Open menu for badge:', id)
}

useHead({ title: 'Display Shelf — Credeny' })
</script>   
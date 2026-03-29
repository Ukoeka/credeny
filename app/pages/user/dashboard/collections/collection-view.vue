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

      <!-- Banner action buttons top-right -->
      <div class="absolute top-4 right-4 z-20 flex flex-col items-center gap-2">
        <button
          @click="shareCollection"
          class="flex items-center gap-1.5 text-xs font-semibold text-[#1a1a2e] bg-white/90 hover:bg-white px-3 py-2 rounded-lg shadow transition-all duration-200 backdrop-blur-sm"
        >
          <svg class="w-3.5 h-3.5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M8.684 13.342C8.886 12.938 9 12.482 9 12c0-.482-.114-.938-.316-1.342m0 2.684a3 3 0 110-2.684m0 2.684l6.632 3.316m-6.632-6l6.632-3.316m0 0a3 3 0 105.367-2.684 3 3 0 00-5.367 2.684zm0 9.316a3 3 0 105.368 2.684 3 3 0 00-5.368-2.684z"/>
          </svg>
          Share Collection
        </button>
        <button
          @click="showAddBadgeModal = true"
          class="flex items-center gap-1.5 text-xs font-semibold text-[#1a1a2e] bg-white/90 hover:bg-white px-3 py-2 rounded-lg shadow transition-all duration-200 backdrop-blur-sm"
        >
          <svg class="w-3.5 h-3.5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 4v16m8-8H4"/>
          </svg>
          Add Badge
        </button>
      </div>

      <div class="relative z-10 text-center">
        <h1 class="text-4xl lg:text-5xl font-extrabold text-white tracking-tight">Work Badges</h1>
        <p class="text-white mt-1">All your badges and achievements in one place</p>
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
      <NuxtLink
        v-for="badge in badges"
        :key="badge.id"
        class="bg-[#FFF7EE] rounded-2xl p-10 border border-[#f0e6d8] hover:shadow-md hover:-translate-y-0.5 transition-all duration-200 cursor-pointer group"
        :to="`/user/dashboard/badge/${badge.id}`"
      >
        <div class="flex justify-center mb-3">
          <img
            :src="badge.image"
            :alt="badge.title"
            class="w-full h-auto rounded-full object-cover border-4 border-[#f5ede3] group-hover:border-[#c8873a] transition-colors duration-200"
          />
        </div>
        <div class="flex items-start justify-between gap-1">
          <div class="min-w-0">
            <h3 class="font-bold text-[#1a1a2e] truncate">{{ badge.title }}</h3>
            <p class="text-xs text-[#888] leading-relaxed mt-0.5 line-clamp-2">{{ badge.description }}</p>
            <p class="text-xs text-[#aaa] mt-2">{{ badge.date }}</p>
          </div>
          <button
            class="flex-shrink-0 p-1 rounded-md hover:bg-[#f0e6d8] transition-colors duration-200 mt-0.5"
            @click.stop="openMenu(badge.id)"
          >
            <svg class="w-4 h-4 text-[#aaa]" fill="currentColor" viewBox="0 0 24 24">
              <path d="M12 13a1 1 0 110-2 1 1 0 010 2zm0-5a1 1 0 110-2 1 1 0 010 2zm0 10a1 1 0 110-2 1 1 0 010 2z"/>
            </svg>
          </button>
        </div>
      </NuxtLink>
    </div>

    <!-- ══════════════════════════════════════
         ADD BADGE MODAL
    ══════════════════════════════════════ -->
    <Teleport to="body">
      <div
        v-if="showAddBadgeModal"
        class="fixed inset-0 z-50 flex items-center justify-center px-4 py-6"
        @click.self="showAddBadgeModal = false"
      >
        <!-- Backdrop -->
        <div class="absolute inset-0 bg-black/50 backdrop-blur-sm" @click="showAddBadgeModal = false"></div>

        <!-- Modal panel -->
        <div class="relative bg-white rounded-3xl shadow-2xl w-full max-w-[780px] max-h-[90vh] flex flex-col z-10 overflow-hidden">

          <!-- Header -->
          <div class="px-8 pt-8 pb-4 flex-shrink-0">
            <h2 class="text-xl font-extrabold text-[#1a1a2e] text-center tracking-tight">
              Select Badge To Add To Collection
            </h2>
          </div>

          <!-- Scrollable badge grid -->
          <div class="flex-1 overflow-y-auto px-8 pb-4">
            <div class="grid grid-cols-2 sm:grid-cols-4 gap-4">
              <div
                v-for="badge in availableBadges"
                :key="badge.id"
                class="relative rounded-2xl p-4 border-2 cursor-pointer transition-all duration-200 select-none"
                :class="isSelected(badge.id)
                  ? 'bg-[#d6edff] border-[#5aabf5]'
                  : 'bg-[#fdf9f5] border-transparent hover:border-[#e0d5c8]'"
                @click="toggleBadge(badge.id)"
              >
                <!-- Toggle indicator — top left -->
                <div class="absolute top-3 left-3 z-10">
                  <!-- Selected: blue square -->
                  <div
                    v-if="isSelected(badge.id)"
                    class="w-5 h-5 rounded-md bg-[#3b9eff] flex items-center justify-center"
                  >
                    <svg class="w-3 h-3 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="3">
                      <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7"/>
                    </svg>
                  </div>
                  <!-- Already in collection: minus -->
                  <div
                    v-else
                    class="w-5 h-5 rounded-md bg-white border border-[#ddd] flex items-center justify-center shadow-sm"
                  >
                    <svg class="w-3 h-3 text-[#aaa]" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                      <path stroke-linecap="round" stroke-linejoin="round" d="M20 12H4"/>
                    </svg>
                  </div>
                </div>

                <!-- Badge image -->
                <div class="flex justify-center mb-3 mt-1">
                  <img
                    :src="badge.image"
                    :alt="badge.title"
                    class="w-full aspect-square rounded-full object-cover"
                  />
                </div>

                <!-- Info -->
                <div>
                  <h3 class="font-bold text-base text-[#1a1a2e] mb-1">{{ badge.title }}</h3>
                  <p class="text-xs text-[#888] leading-relaxed line-clamp-3 mb-2">{{ badge.description }}</p>
                  <div class="flex items-center justify-between">
                    <p class="text-xs text-[#aaa]">{{ badge.date }}</p>
                    <button
                      class="w-6 h-6 flex items-center justify-center rounded hover:bg-[#f0e6d8] transition-colors duration-200"
                      @click.stop="shareBadge(badge.id)"
                    >
                      <svg class="w-3.5 h-3.5 text-[#bbb]" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M8.684 13.342C8.886 12.938 9 12.482 9 12c0-.482-.114-.938-.316-1.342m0 2.684a3 3 0 110-2.684m0 2.684l6.632 3.316m-6.632-6l6.632-3.316m0 0a3 3 0 105.367-2.684 3 3 0 00-5.367 2.684zm0 9.316a3 3 0 105.368 2.684 3 3 0 00-5.368-2.684z"/>
                      </svg>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Footer: Award button -->
          <div class="px-8 py-5 flex-shrink-0 border-t border-[#f0e6d8]">
            <button
              @click="handleAward"
              :disabled="selectedBadgeIds.length === 0 || awarding"
              class="w-full bg-[#1a1a2e] hover:bg-[#2d2d4e] text-white font-bold text-sm py-4 rounded-2xl transition-all duration-200 hover:-translate-y-px disabled:opacity-50 disabled:cursor-not-allowed"
            >
              <span v-if="awarding">Adding...</span>
              <span v-else>
                Award{{ selectedBadgeIds.length > 0 ? ` (${selectedBadgeIds.length})` : '' }}
              </span>
            </button>
          </div>

        </div>
      </div>
    </Teleport>

  </div>
</template>

<script setup>
definePageMeta({ layout: 'dashboard' })

const showAddBadgeModal = ref(false)
const selectedBadgeIds = ref([])
const awarding = ref(false)

// ── Collection badges (already in this collection) ──
const badges = ref([
  { id: 1, title: 'Design Degree I', description: 'Certificate of Completion in design and Visual Asset Production', date: '4th April 2024', image: '/images/randoms/badge.png' },
  { id: 2, title: 'Design Degree II', description: 'Certificate of Completion in design and Visual Asset Production', date: '4th April 2024', image: '/images/randoms/badge.png' },
  { id: 3, title: 'Design Degree I', description: 'Certificate of Completion in design and Visual Asset Production', date: '4th April 2024', image: '/images/randoms/badge.png' },
  { id: 4, title: 'Design Degree I', description: 'Certificate of Completion in design and Visual Asset Production', date: '4th April 2024', image: '/images/randoms/badge.png' },
  { id: 5, title: 'Recycle Course', description: 'Certificate of completion Issued By Max Foundation', date: '4th April 2024', image: '/images/randoms/badge.png' },
  { id: 6, title: 'Design Degree I', description: 'Certificate of Completion in design and Visual Asset Production', date: '4th April 2024', image: '/images/randoms/badge.png' },
  { id: 7, title: 'Design Degree I', description: 'Certificate of Completion in design and Visual Asset Production', date: '4th April 2024', image: '/images/randoms/badge.png' },
  { id: 8, title: 'Design Degree I', description: 'Certificate of Completion in design and Visual Asset Production', date: '4th April 2024', image: '/images/randoms/badge.png' },
])

// ── All available badges from the user's shelf (shown in modal) ──
const availableBadges = ref([
  { id: 101, title: 'Dragon Rider', description: 'Potter ipsum wand elf parchment wingardium. Gnomes good butter mudbloods impedimenta.', date: '4th april 2024', image: '/images/randoms/badge.png' },
  { id: 102, title: 'Dragon Rider', description: 'Potter ipsum wand elf parchment wingardium. Gnomes good butter mudbloods impedimenta.', date: '4th april 2024', image: '/images/randoms/badge.png' },
  { id: 103, title: 'Dragon Rider', description: 'Potter ipsum wand elf parchment wingardium. Gnomes good butter mudbloods impedimenta.', date: '4th april 2024', image: '/images/randoms/badge.png' },
  { id: 104, title: 'Dragon Rider', description: 'Potter ipsum wand elf parchment wingardium. Gnomes good butter mudbloods impedimenta.', date: '4th april 2024', image: '/images/randoms/badge.png' },
  { id: 105, title: 'Dragon Rider', description: 'Potter ipsum wand elf parchment wingardium. Gnomes good butter mudbloods impedimenta.', date: '4th april 2024', image: '/images/randoms/badge.png' },
  { id: 106, title: 'Dragon Rider', description: 'Potter ipsum wand elf parchment wingardium. Gnomes good butter mudbloods impedimenta.', date: '4th april 2024', image: '/images/randoms/badge.png' },
  { id: 107, title: 'Dragon Rider', description: 'Potter ipsum wand elf parchment wingardium. Gnomes good butter mudbloods impedimenta.', date: '4th april 2024', image: '/images/randoms/badge.png' },
  { id: 108, title: 'Dragon Rider', description: 'Potter ipsum wand elf parchment wingardium. Gnomes good butter mudbloods impedimenta.', date: '4th april 2024', image: '/images/randoms/badge.png' },
])

const isSelected = (id) => selectedBadgeIds.value.includes(id)

const toggleBadge = (id) => {
  const idx = selectedBadgeIds.value.indexOf(id)
  if (idx === -1) {
    selectedBadgeIds.value.push(id)
  } else {
    selectedBadgeIds.value.splice(idx, 1)
  }
}

const handleAward = async () => {
  if (selectedBadgeIds.value.length === 0) return
  awarding.value = true
  try {
    
    console.log('Adding badges:', selectedBadgeIds.value)
    selectedBadgeIds.value = []
    showAddBadgeModal.value = false
  } catch (e) {
    console.error('Failed to add badges:', e)
  } finally {
    awarding.value = false
  }
}

const openMenu = (id) => {
  console.log('Open menu for badge:', id)
}

const shareCollection = () => {
  console.log('Share collection')
}

const shareBadge = (id) => {
  console.log('Share badge:', id)
}

useHead({ title: 'Display Collection — Credeny' })
</script>
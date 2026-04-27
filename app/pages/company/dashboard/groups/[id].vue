<template>
  <div>

    <!-- ── Hero Banner ── -->
    <div class="relative w-full rounded-2xl overflow-hidden mb-8 h-[130px] flex items-center justify-center">
      <img src="@/assets/images/backgrounds/dashboard-banner.png" alt="" class="absolute inset-0 w-full h-full object-cover" />
      <div class="absolute inset-0 bg-black/20"></div>

      <!-- Action buttons top-right -->
      <div class="absolute top-3 right-4 z-20 flex flex-col gap-2">
        <button
          @click="showAwardModal = true"
          :disabled="selectedIds.length === 0"
          class="flex items-center gap-2 text-xs font-semibold text-[#1a1a2e] bg-white/90 hover:bg-white px-3 py-2 rounded-lg shadow transition-all duration-200 backdrop-blur-sm whitespace-nowrap disabled:opacity-50 disabled:cursor-not-allowed"
        >
          Grant Award
          <div class="w-5 h-5 rounded-full bg-[#1a1a2e] flex items-center justify-center flex-shrink-0">
            <svg class="w-3 h-3 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="3">
              <path stroke-linecap="round" stroke-linejoin="round" d="M12 4v16m8-8H4"/>
            </svg>
          </div>
        </button>
        <NuxtLink
          :to="`/company/dashboard/groups/edit/${route.params.id}`"
          class="flex items-center gap-2 text-xs font-semibold text-[#1a1a2e] bg-white/90 hover:bg-white px-3 py-2 rounded-lg shadow transition-all duration-200 backdrop-blur-sm whitespace-nowrap"
        >
          Edit Group
          <svg class="w-3.5 h-3.5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
            <path stroke-linecap="round" stroke-linejoin="round" d="M15.232 5.232l3.536 3.536M9 13l6.586-6.586a2 2 0 112.828 2.828L11.828 15.828a2 2 0 01-1.414.586H8v-2.414a2 2 0 01.586-1.414z"/>
          </svg>
        </NuxtLink>
      </div>

      <div class="relative z-10 text-center">
        <h1 class="text-3xl lg:text-4xl font-extrabold text-white tracking-tight">Learning Group 2</h1>
      </div>
    </div>

    <!-- ── Table card ── -->
    <div class="bg-white rounded-2xl border border-[#f0e6d8] overflow-hidden">
      <div class="overflow-x-auto">
        <table class="w-full text-sm">
          <thead>
            <tr class="border-b border-[#f0e6d8]">
              <!-- Select all checkbox -->
              <th class="px-4 py-4 w-10">
                <input
                  type="checkbox"
                  :checked="allSelected"
                  :indeterminate="someSelected"
                  class="w-4 h-4 rounded accent-[#1a1a2e] cursor-pointer"
                  @change="toggleAll"
                />
              </th>
              <th class="text-left px-2 py-4 text-xs font-semibold text-[#aaa] w-[90px]">Serial Number</th>
              <th class="text-left px-4 py-4 text-xs font-semibold text-[#aaa] cursor-pointer hover:text-[#1a1a2e] transition-colors duration-200" @click="sortAwardees">
                <div class="flex items-center gap-1">Name
                  <svg class="w-3 h-3" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7"/>
                  </svg>
                </div>
              </th>
              <th class="text-left px-4 py-4 text-xs font-semibold text-[#aaa]">Email</th>
              <th class="text-left px-4 py-4 text-xs font-semibold text-[#aaa]">Date Added</th>
              <th class="text-left px-4 py-4 text-xs font-semibold text-[#aaa]">Awards Awarded</th>
              <th class="text-left px-4 py-4 text-xs font-semibold text-[#aaa]">Group</th>
              <th class="w-8"></th>
            </tr>
          </thead>
          <tbody class="divide-y divide-[#f7f0e8]">
            <tr
              v-for="(awardee, i) in awardees"
              :key="awardee.id"
              class="transition-colors duration-150 group"
              :class="isSelected(awardee.id) ? 'bg-[#f0f7ff]' : 'hover:bg-[#fdf9f5]'"
            >
              <!-- Checkbox -->
              <td class="px-4 py-4">
                <input
                  type="checkbox"
                  :checked="isSelected(awardee.id)"
                  class="w-4 h-4 rounded accent-[#3b9eff] cursor-pointer"
                  @change="toggleSelect(awardee.id)"
                />
              </td>
              <td class="px-2 py-4 text-xs text-[#aaa]">{{ i + 1 }}</td>
              <td class="px-4 py-4 font-bold text-[#1a1a2e] whitespace-nowrap">{{ awardee.name }}</td>
              <td class="px-4 py-4 text-[#888] whitespace-nowrap">{{ awardee.email }}</td>
              <td class="px-4 py-4 text-[#888] whitespace-nowrap">{{ awardee.dateAdded }}</td>
              <td class="px-4 py-4 text-[#555] text-center">{{ awardee.awardsAwarded }}</td>
              <td class="px-4 py-4">
                <div class="relative inline-block">
                  <select
                    v-model="awardee.group"
                    class="appearance-none bg-transparent text-sm text-[#555] pr-5 cursor-pointer focus:outline-none"
                  >
                    <option v-for="g in groupOptions" :key="g" :value="g">{{ g }}</option>
                  </select>
                  <svg class="absolute right-0 top-1/2 -translate-y-1/2 w-3 h-3 text-[#aaa] pointer-events-none" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7"/>
                  </svg>
                </div>
              </td>
              <td class="px-3 py-4">
                <button class="p-1 rounded-md opacity-0 group-hover:opacity-100 hover:bg-[#f0e6d8] transition-all duration-200">
                  <svg class="w-4 h-4 text-[#aaa]" fill="currentColor" viewBox="0 0 24 24">
                    <path d="M12 13a1 1 0 110-2 1 1 0 010 2zm0-5a1 1 0 110-2 1 1 0 010 2zm0 10a1 1 0 110-2 1 1 0 010 2z"/>
                  </svg>
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <!-- ══════════════════════════════════════
         AWARD BADGE MODAL
    ══════════════════════════════════════ -->
    <Teleport to="body">
      <div
        v-if="showAwardModal"
        class="fixed inset-0 z-50 flex items-center justify-center px-4 py-6"
        @click.self="showAwardModal = false"
      >
        <div class="absolute inset-0 bg-black/50 backdrop-blur-sm" @click="showAwardModal = false"></div>

        <div class="relative bg-white rounded-3xl shadow-2xl w-full max-w-[780px] max-h-[90vh] flex flex-col z-10 overflow-hidden">

          <!-- Header -->
          <div class="px-8 pt-7 pb-4 flex-shrink-0">
            <h2 class="text-xl font-extrabold text-[#1a1a2e] text-center tracking-tight">Award badge</h2>
          </div>

          <!-- Badge grid -->
          <div class="flex-1 overflow-y-auto px-8 pb-4">
            <div class="grid grid-cols-2 sm:grid-cols-4 gap-4">
              <div
                v-for="badge in availableBadges"
                :key="badge.id"
                class="relative rounded-2xl p-4 border-2 cursor-pointer transition-all duration-200 select-none"
                :class="isBadgeSelected(badge.id)
                  ? 'bg-[#d6edff] border-[#5aabf5]'
                  : 'bg-[#fdf9f5] border-transparent hover:border-[#e0d5c8]'"
                @click="toggleBadge(badge.id)"
              >
                <!-- Toggle indicator -->
                <div class="absolute top-3 left-3 z-10">
                  <div v-if="isBadgeSelected(badge.id)" class="w-5 h-5 rounded-md bg-[#3b9eff] flex items-center justify-center">
                    <svg class="w-3 h-3 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="3">
                      <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7"/>
                    </svg>
                  </div>
                  <div v-else class="w-5 h-5 rounded-md bg-white border border-[#ddd] flex items-center justify-center shadow-sm">
                    <svg class="w-3 h-3 text-[#aaa]" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                      <path stroke-linecap="round" stroke-linejoin="round" d="M20 12H4"/>
                    </svg>
                  </div>
                </div>

                <div class="flex justify-center mb-3 mt-1">
                  <img :src="badge.image" :alt="badge.title" class="w-full aspect-square rounded-full object-cover" />
                </div>
                <div>
                  <h3 class="font-bold text-base text-[#1a1a2e] mb-1">{{ badge.title }}</h3>
                  <p class="text-xs text-[#888] leading-relaxed line-clamp-3 mb-2">{{ badge.description }}</p>
                  <div class="flex items-center justify-between">
                    <p class="text-xs text-[#aaa]">{{ badge.date }}</p>
                    <button class="w-6 h-6 flex items-center justify-center rounded hover:bg-[#f0e6d8]" @click.stop>
                      <svg class="w-3.5 h-3.5 text-[#bbb]" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M8.684 13.342C8.886 12.938 9 12.482 9 12c0-.482-.114-.938-.316-1.342m0 2.684a3 3 0 110-2.684m0 2.684l6.632 3.316m-6.632-6l6.632-3.316m0 0a3 3 0 105.367-2.684 3 3 0 00-5.367 2.684zm0 9.316a3 3 0 105.368 2.684 3 3 0 00-5.368-2.684z"/>
                      </svg>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Footer -->
          <div class="px-8 py-5 flex-shrink-0 border-t border-[#f0e6d8]">
            <button
              @click="handleAward"
              :disabled="selectedBadgeIds.length === 0 || awarding"
              class="w-full bg-[#1a1a2e] hover:bg-[#2d2d4e] text-white font-bold text-sm py-4 rounded-2xl transition-all duration-200 hover:-translate-y-px disabled:opacity-50 disabled:cursor-not-allowed"
            >
              <span v-if="awarding">Awarding...</span>
              <span v-else>Award{{ selectedBadgeIds.length > 0 ? ` (${selectedBadgeIds.length})` : '' }}</span>
            </button>
          </div>
        </div>
      </div>
    </Teleport>

  </div>
</template>

<script setup>
definePageMeta({ layout: 'companydashboard' })

const route = useRoute()
const showAwardModal = ref(false)
const selectedIds = ref([])
const selectedBadgeIds = ref([])
const awarding = ref(false)

const groupOptions = ['Learning Group 1', 'Learning Group 2', 'Learning Group 3']

const awardees = ref(
  Array.from({ length: 14 }, (_, i) => ({
    id: i + 1,
    name: i === 1 ? 'Kinio Holo' : 'Mane Rane',
    email: 'Manarrane@gmail.com',
    dateAdded: '13 April 2024',
    awardsAwarded: i % 2 === 0 ? 5 : 6,
    group: 'Learning Group 2',
  }))
)

const availableBadges = ref(
  Array.from({ length: 8 }, (_, i) => ({
    id: i + 1,
    title: 'Dragon Rider',
    description: 'Potter ipsum wand elf parchment wingardium. Gnomes good butter mudbloods impedimenta.',
    date: '4th april 2024',
    image: '/images/randoms/badge.png',
  }))
)

// Awardee selection
const allSelected = computed(() => selectedIds.value.length === awardees.value.length)
const someSelected = computed(() => selectedIds.value.length > 0 && !allSelected.value)
const isSelected = (id) => selectedIds.value.includes(id)
const toggleSelect = (id) => {
  const idx = selectedIds.value.indexOf(id)
  idx === -1 ? selectedIds.value.push(id) : selectedIds.value.splice(idx, 1)
}
const toggleAll = () => {
  selectedIds.value = allSelected.value ? [] : awardees.value.map(a => a.id)
}

// Badge selection
const isBadgeSelected = (id) => selectedBadgeIds.value.includes(id)
const toggleBadge = (id) => {
  const idx = selectedBadgeIds.value.indexOf(id)
  idx === -1 ? selectedBadgeIds.value.push(id) : selectedBadgeIds.value.splice(idx, 1)
}

const handleAward = async () => {
  awarding.value = true
  try {
    // API call: award selectedBadgeIds to selectedIds (awardees)
    console.log('Awarding badges', selectedBadgeIds.value, 'to awardees', selectedIds.value)
    selectedBadgeIds.value = []
    showAwardModal.value = false
  } finally {
    awarding.value = false
  }
}

const sortAwardees = () => {
  awardees.value.sort((a, b) => a.name.localeCompare(b.name))
}

useHead({ title: 'Learning Group 2 — Credeny Issuer' })
</script>
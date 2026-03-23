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
      <div class="absolute top-4 right-4 z-20 flex items-center gap-2">
        <button
          @click="showCreateModal = true"
          class="text-xs font-semibold text-[#1a1a2e] bg-white/90 hover:bg-white px-3 py-1.5 rounded-lg shadow transition-all duration-200 backdrop-blur-sm"
        >
          Create Collection
        </button>
        <button
          @click="showEditModal = true"
          class="text-xs font-semibold text-[#1a1a2e] bg-white/90 hover:bg-white px-3 py-1.5 rounded-lg shadow transition-all duration-200 backdrop-blur-sm"
        >
          Edit Collection
        </button>
      </div>

      <div class="relative z-10 text-center">
        <h1 class="text-4xl lg:text-5xl font-extrabold text-[#1a1a2e] tracking-tight">Badge Collections</h1>
        <p class=" text-[#333] mt-1">Organize your badges for easy identification</p>
      </div>
    </div>

    <!-- ── EMPTY STATE ── -->
    <div v-if="collections.length === 0" class="flex flex-col items-center justify-center px-20 py-24">
      <img
        src="@/assets/images/randoms/web.png"
        alt="No collections"
        class="w-52 h-52 object-contain opacity-60 mb-6"
      />
      <p class="text-lg font-semibold text-[#c8b89a]">No Collections Yet</p>
    </div>

    <!-- ── POPULATED STATE ── -->
    <div v-else class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-6">
      <NuxtLink
        v-for="collection in collections"
        :key="collection.id"
        :to="`/user/dashboard/collection/${collection.id}`"
        class="bg-white rounded-2xl p-4 border border-[#f0e6d8] hover:shadow-md hover:-translate-y-0.5 transition-all duration-200 cursor-pointer group block"
      >
        <!-- 3x3 badge thumbnail grid -->
        <div class="grid grid-cols-3 gap-1.5 mb-4">
          <template v-for="n in 9" :key="n">
            <!-- Filled slot -->
            <img
              v-if="collection.badges[n - 1]"
              :src="collection.badges[n - 1].image"
              :alt="collection.badges[n - 1].title"
              class="w-full aspect-square rounded-full object-cover"
            />
            <!-- Empty slot -->
            <div
              v-else
              class="w-full aspect-square rounded-full bg-[#f0e6d8]"
            ></div>
          </template>
        </div>

        <!-- Collection info -->
        <div class="flex items-end justify-between gap-2">
          <div class="min-w-0">
            <h3 class="font-bold text-sm text-[#1a1a2e] truncate group-hover:text-[#c8873a] transition-colors duration-200">
              {{ collection.name }}
            </h3>
            <p class="text-xs text-[#aaa] mt-0.5">{{ collection.badgeCount }} badges</p>
            <p class="text-xs text-[#bbb] mt-0.5">{{ collection.date }}</p>
          </div>

          <!-- Share icon -->
          <button
            class="flex-shrink-0 w-7 h-7 flex items-center justify-center rounded-md hover:bg-[#f0e6d8] transition-colors duration-200"
            @click.prevent="shareCollection(collection.id)"
          >
            <svg class="w-4 h-4 text-[#bbb] hover:text-[#c8873a] transition-colors duration-200" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round" d="M8.684 13.342C8.886 12.938 9 12.482 9 12c0-.482-.114-.938-.316-1.342m0 2.684a3 3 0 110-2.684m0 2.684l6.632 3.316m-6.632-6l6.632-3.316m0 0a3 3 0 105.367-2.684 3 3 0 00-5.367 2.684zm0 9.316a3 3 0 105.368 2.684 3 3 0 00-5.368-2.684z"/>
            </svg>
          </button>
        </div>
      </NuxtLink>
    </div>

    <!-- ── Create Collection Modal ── -->
    <Teleport to="body">
      <div
        v-if="showCreateModal"
        class="fixed inset-0 z-50 flex items-center justify-center px-4"
        @click.self="showCreateModal = false"
      >
        <div class="absolute inset-0 bg-black/40 backdrop-blur-sm"></div>
        <div class="relative bg-[#f5ede3] rounded-2xl shadow-2xl w-full max-w-md px-8 py-8 z-10">
          <h2 class="text-lg font-extrabold text-[#1a1a2e] mb-6 tracking-tight">Create Collection</h2>

          <div class="space-y-4">
            <div class="flex flex-col gap-1.5">
              <label class="text-xs font-semibold text-[#1a1a2e]">Collection Name</label>
              <input
                v-model="newCollection.name"
                type="text"
                placeholder="e.g. Work Badges"
                class="w-full bg-white border border-[#e0d5c8] rounded-lg px-3.5 py-3 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200"
              />
            </div>
            <div class="flex flex-col gap-1.5">
              <label class="text-xs font-semibold text-[#1a1a2e]">Description <span class="text-[#aaa] font-normal">(optional)</span></label>
              <textarea
                v-model="newCollection.description"
                placeholder="What is this collection about?"
                rows="3"
                class="w-full bg-white border border-[#e0d5c8] rounded-lg px-3.5 py-3 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200 resize-none"
              ></textarea>
            </div>
          </div>

          <div class="flex gap-3 mt-6">
            <button
              @click="showCreateModal = false"
              class="flex-1 text-sm font-semibold text-[#1a1a2e] py-3 rounded-xl border border-[#1a1a2e]/20 hover:bg-[#1a1a2e]/5 transition-all duration-200"
            >
              Cancel
            </button>
            <button
              @click="handleCreateCollection"
              class="flex-1 text-sm font-bold text-white bg-[#1a1a2e] hover:bg-[#2d2d4e] py-3 rounded-xl transition-all duration-200 hover:-translate-y-px"
            >
              Create
            </button>
          </div>
        </div>
      </div>
    </Teleport>

  </div>
</template>

<script setup>
definePageMeta({ layout: 'dashboard' })

const showCreateModal = ref(false)
const showEditModal = ref(false)

const newCollection = ref({
  name: '',
  description: '',
})

// Replace with real API data
const collections = ref([
  {
    id: 1,
    name: 'Work Badges',
    badgeCount: 16,
    date: '4th April 2024',
    badges: Array(9).fill({ image: '/images/randoms/badge.png', title: 'Badge' }),
  },
  {
    id: 2,
    name: 'School Badges',
    badgeCount: 8,
    date: '4th April 2024',
    badges: Array(6).fill({ image: '/images/randoms/badge.png', title: 'Badge' }),
  },
  {
    id: 3,
    name: 'Life Things',
    badgeCount: 5,
    date: '4th April 2024',
    badges: Array(3).fill({ image: '/images/randoms/badge.png', title: 'Badge' }),
  },
  {
    id: 4,
    name: 'Atero Badges',
    badgeCount: 16,
    date: '4th April 2024',
    badges: Array(9).fill({ image: '/images/randoms/badge.png', title: 'Badge' }),
  },
  {
    id: 5,
    name: 'Achievements',
    badgeCount: 16,
    date: '4th April 2024',
    badges: Array(9).fill({ image: '/images/randoms/badge.png', title: 'Badge' }),
  },
  {
    id: 6,
    name: "Favour's",
    badgeCount: 16,
    date: '4th April 2024',
    badges: Array(9).fill({ image: '/images/randoms/badge.png', title: 'Badge' }),
  },
  {
    id: 7,
    name: 'Credeny Private',
    badgeCount: 16,
    date: '4th April 2024',
    badges: Array(9).fill({ image: '/images/randoms/badge.png', title: 'Badge' }),
  },
  {
    id: 8,
    name: 'Merits',
    badgeCount: 16,
    date: '4th April 2024',
    badges: Array(9).fill({ image: '/images/randoms/badge.png', title: 'Badge' }),
  },
])

const shareCollection = (id) => {
  // Add share logic here
  console.log('Share collection:', id)
}

const handleCreateCollection = () => {
  if (!newCollection.value.name) return
  // Add your create collection API call here
  console.log('Creating collection:', newCollection.value)
  newCollection.value = { name: '', description: '' }
  showCreateModal.value = false
}

useHead({ title: 'Badge Collections — Credeny' })
</script>
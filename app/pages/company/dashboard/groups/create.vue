<template>
  <div>

    <!-- Page heading -->
    <div class="flex items-center gap-3 mb-8">
      <button
        @click="$router.back()"
        class="flex items-center justify-center w-8 h-8 rounded-full bg-[#1a1a2e] hover:bg-[#2d2d4e] text-white transition-colors duration-200 flex-shrink-0"
      >
        <svg class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
          <path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7"/>
        </svg>
      </button>
      <h1 class="text-xl font-extrabold text-[#1a1a2e] tracking-tight">Create new Group</h1>
    </div>

    <!-- Form card -->
    <div class="bg-[#faf5ee] rounded-2xl border border-dashed border-[#e0d5c8] px-8 py-8 max-w-[780px]">
      <div class="space-y-7">

        <!-- Group Name -->
        <div class="flex flex-col gap-1.5">
          <label class="text-sm font-semibold text-[#1a1a2e]">Group Name</label>
          <input
            v-model="form.name"
            type="text"
            placeholder="Placeholder"
            class="w-full sm:w-[260px] bg-white border border-[#e0d5c8] rounded-lg px-4 py-3 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200"
          />
        </div>

        <!-- Banner Image picker -->
        <div class="flex flex-col gap-3">
          <label class="text-sm font-semibold text-[#1a1a2e]">Banner Image</label>
          <div class="flex items-center gap-3 flex-wrap">
            <button
              v-for="(banner, i) in bannerOptions"
              :key="i"
              type="button"
              class="relative w-[110px] h-[80px] rounded-xl overflow-hidden border-[3px] transition-all duration-200 flex-shrink-0 focus:outline-none"
              :class="form.selectedBanner === i
                ? 'border-[#c8873a] shadow-lg scale-[1.04]'
                : 'border-transparent hover:border-[#c8873a]/40 hover:scale-[1.02]'"
              @click="form.selectedBanner = i"
            >
              <img :src="banner.src" :alt="banner.alt" class="w-full h-full object-cover" />
              <div v-if="form.selectedBanner === i" class="absolute top-1.5 right-1.5 w-5 h-5 rounded-full bg-[#c8873a] flex items-center justify-center">
                <svg class="w-3 h-3 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="3">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7"/>
                </svg>
              </div>
            </button>

            <!-- Upload custom -->
            <label class="w-[110px] h-[80px] rounded-xl border-2 border-dashed border-[#e0d5c8] hover:border-[#c8873a] flex flex-col items-center justify-center gap-1 cursor-pointer transition-colors duration-200 flex-shrink-0 group">
              <svg class="w-5 h-5 text-[#ccc] group-hover:text-[#c8873a] transition-colors duration-200" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 4v16m8-8H4"/>
              </svg>
              <span class="text-[10px] text-[#ccc] group-hover:text-[#c8873a] font-medium transition-colors duration-200">Upload</span>
              <input type="file" accept="image/*" class="hidden" @change="handleCustomBanner" />
            </label>
          </div>
        </div>

      </div>

      <p v-if="errorMsg" class="text-xs text-red-500 mt-5">{{ errorMsg }}</p>

      <!-- Actions -->
      <div class="flex items-center gap-3 mt-8">
        <button
          @click="$router.back()"
          class="text-sm font-semibold text-[#1a1a2e] px-6 py-2.5 rounded-lg border border-[#1a1a2e]/25 hover:bg-[#1a1a2e]/5 transition-all duration-200"
        >
          Cancel
        </button>
        <button
          @click="handleSave"
          :disabled="loading"
          class="text-sm font-bold text-white bg-[#1a1a2e] hover:bg-[#2d2d4e] px-6 py-2.5 rounded-lg transition-all duration-200 hover:-translate-y-px disabled:opacity-60 disabled:cursor-not-allowed"
        >
          <span v-if="loading">Saving...</span>
          <span v-else>Save Group</span>
        </button>
      </div>
    </div>

  </div>
</template>

<script setup>
definePageMeta({ layout: 'companydashboard' })

const loading = ref(false)
const errorMsg = ref('')

const form = ref({
  name: '',
  selectedBanner: 0,
  customBanner: null,
})

const bannerOptions = [
  { src: '/images/banners/banner-1.png', alt: 'Blue waves' },
  { src: '/images/banners/banner-2.png', alt: 'Coloured stripes' },
  { src: '/images/banners/banner-3.png', alt: 'Abstract paint' },
  { src: '/images/banners/banner-4.png', alt: 'Green yellow flow' },
  { src: '/images/banners/banner-5.png', alt: 'Pink marble' },
]

const handleCustomBanner = (e) => {
  const file = e.target.files[0]
  if (!file) return
  form.value.customBanner = file
  form.value.selectedBanner = null
}

const handleSave = async () => {
  errorMsg.value = ''
  if (!form.value.name.trim()) {
    errorMsg.value = 'Please enter a group name.'
    return
  }
  loading.value = true
  try {
    // Add your API call here
    await navigateTo('/company/dashboard/groups')
  } catch (e) {
    errorMsg.value = 'Something went wrong. Please try again.'
  } finally {
    loading.value = false
  }
}

useHead({ title: 'Create Group — Credeny Issuer' })
</script>
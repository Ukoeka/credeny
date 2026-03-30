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
      <h1 class="text-xl font-extrabold text-[#1a1a2e] tracking-tight">Create new Badge</h1>
    </div>

    <!-- Form card -->
    <div class="bg-[#faf5ee] w-full rounded-2xl border border-dashed border-[#e0d5c8] px-8 py-8">
      <div class="space-y-6">

        <!-- Badge Name -->
        <div class="flex flex-col gap-1.5">
          <label class="text-sm font-semibold text-[#1a1a2e]">Badge Name</label>
          <input
            v-model="form.name"
            type="text"
            placeholder="Placeholder"
            class="w-full lg:w-[50%] bg-white border border-[#e0d5c8] rounded-lg px-4 py-5 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200"
          />
        </div>

        <!-- Image Upload -->
        <div class="flex flex-col gap-2">
          <label class="text-sm font-semibold text-[#1a1a2e]">Image Upload</label>

          <label class="cursor-pointer w-[180px]">
            <div
              class="bg-white border border-[#e0d5c8] rounded-xl p-4 flex flex-col items-center justify-center gap-3 hover:border-[#c8873a] transition-all duration-200 group min-h-[120px]"
              :class="dragOver ? 'border-[#c8873a] bg-[#fdf9f5] scale-[1.01]' : ''"
              @dragover.prevent="dragOver = true"
              @dragleave="dragOver = false"
              @drop.prevent="handleDrop"
            >
              <!-- Preview -->
              <div v-if="form.imagePreview" class="flex flex-col items-center gap-2">
                <img
                  :src="form.imagePreview"
                  alt="Badge preview"
                  class="w-16 h-16 rounded-full object-cover border-2 border-[#e0d5c8]"
                />
                <span class="text-[10px] text-[#aaa] font-medium">Click to change</span>
              </div>

              <!-- Placeholder -->
              <div v-else class="flex flex-col items-center gap-2">
                <span class="text-xs text-[#aaa] font-medium">Drag and drop image</span>
                <div class="w-12 h-12 rounded-xl border border-[#e0d5c8] flex items-center justify-center bg-[#f5ede3]">
                  <svg class="w-6 h-6 text-[#c8c0b5] group-hover:text-[#c8873a] transition-colors duration-200" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                    <rect x="3" y="3" width="18" height="18" rx="3" stroke-width="1.5"/>
                    <circle cx="8.5" cy="8.5" r="1.5"/>
                    <path stroke-linecap="round" stroke-linejoin="round" d="M21 15l-5-5L5 21"/>
                  </svg>
                </div>
                <span class="text-xs text-[#c8873a] font-semibold group-hover:underline">
                  Or Search for Image
                </span>
              </div>
            </div>
            <input
              type="file"
              accept="image/*"
              class="hidden"
              @change="handleFileChange"
            />
          </label>
        </div>

        <!-- Description -->
        <div class="flex flex-col gap-1.5">
          <label class="text-sm font-semibold text-[#1a1a2e]">Description</label>
          <textarea
            v-model="form.description"
            placeholder="Placeholder"
            rows="6"
            class="w-full bg-white border border-[#e0d5c8] rounded-xl px-4 py-3 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200 resize-none"
          ></textarea>
        </div>

        <!-- Earning Criteria -->
        <div class="flex flex-col gap-1.5">
          <label class="text-sm font-semibold text-[#1a1a2e]">Earning Criteria</label>
          <input
            v-model="form.criteria"
            type="text"
            placeholder="Placeholder"
            class="w-full sm:w-[260px] bg-white border border-[#e0d5c8] rounded-lg px-4 py-3 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200"
          />
        </div>

      </div>

      <!-- Error -->
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
          <span v-else>Save Collection</span>
        </button>
      </div>

    </div>
  </div>
</template>

<script setup>
definePageMeta({ layout: 'companydashboard' })

const dragOver = ref(false)
const loading = ref(false)
const errorMsg = ref('')

const form = ref({
  name: '',
  imageFile: null,
  imagePreview: null,
  description: '',
  criteria: '',
})

const handleFileChange = (e) => {
  const file = e.target.files[0]
  if (!file) return
  form.value.imageFile = file
  form.value.imagePreview = URL.createObjectURL(file)
}

const handleDrop = (e) => {
  dragOver.value = false
  const file = e.dataTransfer.files[0]
  if (!file || !file.type.startsWith('image/')) return
  form.value.imageFile = file
  form.value.imagePreview = URL.createObjectURL(file)
}

const handleSave = async () => {
  errorMsg.value = ''

  if (!form.value.name.trim()) {
    errorMsg.value = 'Please enter a badge name.'
    return
  }
  if (!form.value.imageFile) {
    errorMsg.value = 'Please upload a badge image.'
    return
  }

  loading.value = true
  try {
    // Add your API call here
    // e.g. const formData = new FormData()
    // formData.append('name', form.value.name)
    // formData.append('image', form.value.imageFile)
    // formData.append('description', form.value.description)
    // formData.append('criteria', form.value.criteria)
    // await useFetch('/api/badges', { method: 'POST', body: formData })
    await navigateTo('/issuer/dashboard/badges')
  } catch (e) {
    errorMsg.value = 'Something went wrong. Please try again.'
  } finally {
    loading.value = false
  }
}

useHead({ title: 'Create Badge — Credeny' })
</script>
<template>
  <div>

    <!-- ── Hero Banner ── -->
    <div class="relative w-full rounded-2xl overflow-hidden mb-8 h-[130px] flex items-center justify-center">
      <img
        src="@/assets/images/backgrounds/dashboard-banner.png"
        alt=""
        class="absolute inset-0 w-full h-full object-cover"
      />
      <div class="absolute inset-0 bg-black/15"></div>

      <!-- Action buttons top-right -->
      <div class="absolute top-3 right-4 z-20 flex flex-col gap-2">
        <button
          @click="showAddSingleModal = true"
          class="flex items-center gap-2 text-xs font-semibold text-[#1a1a2e] bg-white/90 hover:bg-white px-3 py-2 rounded-lg shadow transition-all duration-200 backdrop-blur-sm whitespace-nowrap"
        >
          Add Single Awardee
          <div class="w-5 h-5 rounded-full bg-[#1a1a2e] flex items-center justify-center flex-shrink-0">
            <svg class="w-3 h-3 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="3">
              <path stroke-linecap="round" stroke-linejoin="round" d="M12 4v16m8-8H4"/>
            </svg>
          </div>
        </button>
        <button
          @click="showBulkModal = true"
          class="flex items-center gap-2 text-xs font-semibold text-[#1a1a2e] bg-white/90 hover:bg-white px-3 py-2 rounded-lg shadow transition-all duration-200 backdrop-blur-sm whitespace-nowrap"
        >
          Bulk Add
          <div class="w-5 h-5 rounded-full bg-[#1a1a2e] flex items-center justify-center flex-shrink-0">
            <svg class="w-3 h-3 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="3">
              <path stroke-linecap="round" stroke-linejoin="round" d="M12 4v16m8-8H4"/>
            </svg>
          </div>
        </button>
      </div>

      <div class="relative z-10 text-center">
        <h1 class="text-3xl lg:text-4xl font-extrabold text-[#1a1a2e] tracking-tight">Awardees</h1>
        <p class="text-[#333] text-sm mt-1">Add or remove awardees, award badges</p>
      </div>
    </div>

    <!-- ── Table card ── -->
    <div class="bg-white rounded-2xl border border-[#f0e6d8] overflow-hidden">
      <div class="overflow-x-auto">
        <table class="w-full text-sm">
          <!-- Head -->
          <thead>
            <tr class="border-b border-[#f0e6d8]">
              <th class="text-left px-5 py-4 text-xs font-semibold text-[#aaa] whitespace-nowrap w-[100px]">
                Serial Number
              </th>
              <th class="text-left px-4 py-4 text-xs font-semibold text-[#aaa] whitespace-nowrap cursor-pointer hover:text-[#1a1a2e] transition-colors duration-200" @click="sortBy('name')">
                <div class="flex items-center gap-1">
                  Name
                  <svg class="w-3 h-3" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7"/>
                  </svg>
                </div>
              </th>
              <th class="text-left px-4 py-4 text-xs font-semibold text-[#aaa] whitespace-nowrap">Email</th>
              <th class="text-left px-4 py-4 text-xs font-semibold text-[#aaa] whitespace-nowrap">Date Added</th>
              <th class="text-left px-4 py-4 text-xs font-semibold text-[#aaa] whitespace-nowrap">Awards Awarded</th>
              <th class="text-left px-4 py-4 text-xs font-semibold text-[#aaa] whitespace-nowrap">Group</th>
              <th class="w-8"></th>
            </tr>
          </thead>

          <!-- Body -->
          <tbody class="divide-y divide-[#f7f0e8]">
            <tr
              v-for="(awardee, i) in awardees"
              :key="awardee.id"
              class="hover:bg-[#fdf9f5] transition-colors duration-150 group"
            >
              <!-- Serial -->
              <td class="px-5 py-4 text-xs text-[#aaa]">{{ i + 1 }}</td>

              <!-- Name -->
              <td class="px-4 py-4 font-bold text-[#1a1a2e] whitespace-nowrap">{{ awardee.name }}</td>

              <!-- Email -->
              <td class="px-4 py-4 text-[#888] whitespace-nowrap">{{ awardee.email }}</td>

              <!-- Date -->
              <td class="px-4 py-4 text-[#888] whitespace-nowrap">{{ awardee.dateAdded }}</td>

              <!-- Awards -->
              <td class="px-4 py-4 text-[#555] text-center">{{ awardee.awardsAwarded }}</td>

              <!-- Group dropdown -->
              <td class="px-4 py-4">
                <div class="relative inline-block">
                  <select
                    v-model="awardee.group"
                    class="appearance-none bg-transparent text-sm text-[#555] pr-5 cursor-pointer focus:outline-none hover:text-[#1a1a2e] transition-colors duration-200"
                  >
                    <option v-for="g in groups" :key="g" :value="g">{{ g }}</option>
                  </select>
                  <svg class="absolute right-0 top-1/2 -translate-y-1/2 w-3 h-3 text-[#aaa] pointer-events-none" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7"/>
                  </svg>
                </div>
              </td>

              <!-- More options -->
              <td class="px-3 py-4">
                <div class="relative">
                  <button
                    class="p-1 rounded-md opacity-0 group-hover:opacity-100 hover:bg-[#f0e6d8] transition-all duration-200"
                    @click="openMenu(awardee.id, $event)"
                  >
                    <svg class="w-4 h-4 text-[#aaa]" fill="currentColor" viewBox="0 0 24 24">
                      <path d="M12 13a1 1 0 110-2 1 1 0 010 2zm0-5a1 1 0 110-2 1 1 0 010 2zm0 10a1 1 0 110-2 1 1 0 010 2z"/>
                    </svg>
                  </button>

                  <!-- Dropdown menu -->
                  <div
                    v-if="openMenuId === awardee.id"
                    class="absolute right-0 top-full mt-1 bg-white rounded-xl shadow-lg border border-[#f0e6d8] z-20 py-1 min-w-[140px]"
                    v-click-outside="closeMenu"
                  >
                    <button class="w-full text-left px-4 py-2 text-xs font-medium text-[#555] hover:bg-[#fdf9f5] hover:text-[#1a1a2e] transition-colors duration-150">
                      View Profile
                    </button>
                    <button class="w-full text-left px-4 py-2 text-xs font-medium text-[#555] hover:bg-[#fdf9f5] hover:text-[#1a1a2e] transition-colors duration-150">
                      Award Badge
                    </button>
                    <button class="w-full text-left px-4 py-2 text-xs font-medium text-red-500 hover:bg-red-50 transition-colors duration-150">
                      Remove
                    </button>
                  </div>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <!-- ══════════════════════════════════════
         ADD SINGLE AWARDEE MODAL
    ══════════════════════════════════════ -->
    <Teleport to="body">
      <div
        v-if="showAddSingleModal"
        class="fixed inset-0 z-50 flex items-center justify-center px-4"
        @click.self="showAddSingleModal = false"
      >
        <div class="absolute inset-0 bg-black/40 backdrop-blur-sm" @click="showAddSingleModal = false"></div>
        <div class="relative bg-[#f5ede3] rounded-2xl shadow-2xl w-full max-w-md px-8 py-8 z-10">
          <h2 class="text-lg font-extrabold text-[#1a1a2e] mb-6 tracking-tight">Add Single Awardee</h2>

          <div class="space-y-4">
            <div class="flex flex-col gap-1.5">
              <label class="text-xs font-semibold text-[#1a1a2e]">Full Name</label>
              <input v-model="singleForm.name" type="text" placeholder="e.g. Mane Rane"
                class="w-full bg-white border border-[#e0d5c8] rounded-lg px-3.5 py-3 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200" />
            </div>
            <div class="flex flex-col gap-1.5">
              <label class="text-xs font-semibold text-[#1a1a2e]">Email</label>
              <input v-model="singleForm.email" type="email" placeholder="e.g. name@gmail.com"
                class="w-full bg-white border border-[#e0d5c8] rounded-lg px-3.5 py-3 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200" />
            </div>
            <div class="flex flex-col gap-1.5">
              <label class="text-xs font-semibold text-[#1a1a2e]">Group <span class="text-[#aaa] font-normal">(optional)</span></label>
              <select v-model="singleForm.group"
                class="w-full bg-white border border-[#e0d5c8] rounded-lg px-3.5 py-3 text-sm text-[#333] focus:outline-none focus:border-[#c8873a] transition-colors duration-200 appearance-none cursor-pointer">
                <option value="">No group</option>
                <option v-for="g in groups" :key="g" :value="g">{{ g }}</option>
              </select>
            </div>
          </div>

          <p v-if="singleError" class="text-xs text-red-500 mt-3">{{ singleError }}</p>

          <div class="flex gap-3 mt-6">
            <button @click="showAddSingleModal = false"
              class="flex-1 text-sm font-semibold text-[#1a1a2e] py-3 rounded-xl border border-[#1a1a2e]/20 hover:bg-[#1a1a2e]/5 transition-all duration-200">
              Cancel
            </button>
            <button @click="handleAddSingle" :disabled="addingSingle"
              class="flex-1 text-sm font-bold text-white bg-[#1a1a2e] hover:bg-[#2d2d4e] py-3 rounded-xl transition-all duration-200 hover:-translate-y-px disabled:opacity-60 disabled:cursor-not-allowed">
              <span v-if="addingSingle">Adding...</span>
              <span v-else>Add Awardee</span>
            </button>
          </div>
        </div>
      </div>
    </Teleport>

    <!-- ══════════════════════════════════════
         BULK ADD MODAL
    ══════════════════════════════════════ -->
    <Teleport to="body">
      <div
        v-if="showBulkModal"
        class="fixed inset-0 z-50 flex items-center justify-center px-4"
        @click.self="showBulkModal = false"
      >
        <div class="absolute inset-0 bg-black/40 backdrop-blur-sm" @click="showBulkModal = false"></div>
        <div class="relative bg-[#f5ede3] rounded-2xl shadow-2xl w-full max-w-md px-8 py-8 z-10">
          <h2 class="text-lg font-extrabold text-[#1a1a2e] mb-2 tracking-tight">Bulk Add Awardees</h2>
          <p class="text-xs text-[#888] mb-6">Upload a CSV file with columns: Name, Email, Group</p>

          <!-- Upload area -->
          <label class="cursor-pointer block mb-5">
            <div
              class="w-full border-2 border-dashed border-[#e0d5c8] hover:border-[#c8873a] rounded-xl py-10 flex flex-col items-center gap-3 transition-all duration-200 group bg-white"
              :class="bulkFile ? 'border-[#c8873a] bg-[#fdf9f5]' : ''"
            >
              <svg class="w-10 h-10 text-[#c8c0b5] group-hover:text-[#c8873a] transition-colors duration-200" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                <path stroke-linecap="round" stroke-linejoin="round" d="M9 13h6m-3-3v6m5 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"/>
              </svg>
              <div class="text-center">
                <p v-if="bulkFile" class="text-sm font-semibold text-[#c8873a]">{{ bulkFile.name }}</p>
                <p v-else class="text-sm text-[#aaa] font-medium">Drop your CSV here or <span class="text-[#c8873a] font-semibold">browse</span></p>
                <p class="text-xs text-[#bbb] mt-1">CSV files only</p>
              </div>
            </div>
            <input type="file" accept=".csv" class="hidden" @change="handleBulkFile" />
          </label>

          <p v-if="bulkError" class="text-xs text-red-500 mb-3">{{ bulkError }}</p>

          <div class="flex gap-3">
            <button @click="showBulkModal = false"
              class="flex-1 text-sm font-semibold text-[#1a1a2e] py-3 rounded-xl border border-[#1a1a2e]/20 hover:bg-[#1a1a2e]/5 transition-all duration-200">
              Cancel
            </button>
            <button @click="handleBulkUpload" :disabled="!bulkFile || uploadingBulk"
              class="flex-1 text-sm font-bold text-white bg-[#1a1a2e] hover:bg-[#2d2d4e] py-3 rounded-xl transition-all duration-200 hover:-translate-y-px disabled:opacity-60 disabled:cursor-not-allowed">
              <span v-if="uploadingBulk">Uploading...</span>
              <span v-else>Upload</span>
            </button>
          </div>
        </div>
      </div>
    </Teleport>

  </div>
</template>

<script setup>
definePageMeta({ layout: 'companydashboard' })

// ── Menu state ──
const openMenuId = ref(null)
const openMenu = (id) => { openMenuId.value = openMenuId.value === id ? null : id }
const closeMenu = () => { openMenuId.value = null }

// ── Modal state ──
const showAddSingleModal = ref(false)
const showBulkModal = ref(false)

// ── Single awardee form ──
const singleForm = ref({ name: '', email: '', group: '' })
const singleError = ref('')
const addingSingle = ref(false)

// ── Bulk upload ──
const bulkFile = ref(null)
const bulkError = ref('')
const uploadingBulk = ref(false)

// ── Groups ──
const groups = ref(['Learning Group 1', 'Learning Group 2', 'Learning Group 3', 'Learning Group 4'])

// ── Awardees data — replace with real API ──
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

const handleAddSingle = async () => {
  singleError.value = ''
  if (!singleForm.value.name.trim() || !singleForm.value.email.trim()) {
    singleError.value = 'Please fill in name and email.'
    return
  }
  addingSingle.value = true
  try {
    // Add your API call here
    awardees.value.unshift({
      id: Date.now(),
      name: singleForm.value.name,
      email: singleForm.value.email,
      dateAdded: new Date().toLocaleDateString('en-GB', { day: 'numeric', month: 'long', year: 'numeric' }),
      awardsAwarded: 0,
      group: singleForm.value.group || 'Learning Group 1',
    })
    singleForm.value = { name: '', email: '', group: '' }
    showAddSingleModal.value = false
  } catch (e) {
    singleError.value = 'Something went wrong. Please try again.'
  } finally {
    addingOnly.value = false
  }
}

const handleBulkFile = (e) => {
  bulkFile.value = e.target.files[0] || null
  bulkError.value = ''
}

const handleBulkUpload = async () => {
  if (!bulkFile.value) return
  bulkError.value = ''
  uploadingBulk.value = true
  try {
    // Add your CSV upload API call here
    // const formData = new FormData()
    // formData.append('file', bulkFile.value)
    // await useFetch('/api/awardees/bulk', { method: 'POST', body: formData })
    bulkFile.value = null
    showBulkModal.value = false
  } catch (e) {
    bulkError.value = 'Upload failed. Please check your CSV and try again.'
  } finally {
    uploadingBulk.value = false
  }
}

const sortBy = (field) => {
  awardees.value.sort((a, b) => a[field].localeCompare(b[field]))
}

// ── Click outside directive ──
const vClickOutside = {
  mounted(el, binding) {
    el._clickOutside = (e) => { if (!el.contains(e.target)) binding.value() }
    document.addEventListener('click', el._clickOutside)
  },
  unmounted(el) {
    document.removeEventListener('click', el._clickOutside)
  },
}

useHead({ title: 'Awardees — Credeny Issuer' })
</script>
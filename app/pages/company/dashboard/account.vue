<template>
  <div>

    <!-- ── Hero Banner ── -->
    <div class="relative w-full rounded-2xl overflow-hidden mb-6 h-[200px] flex items-center justify-center">
      <img
        src="@/assets/images/backgrounds/dashboard-banner.png"
        alt=""
        class="absolute inset-0 w-full h-full object-cover"
      />
      <div class="absolute inset-0 bg-black/15"></div>

      <!-- Edit Profile button -->
      <button
        @click="openEditModal"
        class="absolute top-4 right-4 z-20 flex items-center gap-1.5 text-xs font-semibold text-[#1a1a2e] bg-white/90 hover:bg-white px-3 py-2 rounded-lg shadow transition-all duration-200 backdrop-blur-sm"
      >
        Edit Profile
        <svg class="w-3.5 h-3.5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
          <path stroke-linecap="round" stroke-linejoin="round" d="M15.232 5.232l3.536 3.536M9 13l6.586-6.586a2 2 0 112.828 2.828L11.828 15.828a2 2 0 01-1.414.586H8v-2.414a2 2 0 01.586-1.414z"/>
        </svg>
      </button>

      <div class="relative z-10 text-center">
        <h1 class="text-3xl lg:text-4xl font-extrabold text-[#1a1a2e] tracking-tight">Company Account</h1>
        <p class="text-[#333] text-sm mt-1">Your Credeny account</p>
      </div>
    </div>

    <!-- ── Company info card ── -->
    <div class="bg-white rounded-2xl border border-[#f0e6d8] px-6 py-5 mb-5 flex items-center gap-6">
      <!-- Company logo -->
      <div class="flex-shrink-0">
        <img
          :src="company.logo"
          alt="Company logo"
          class="w-20 h-20 rounded-full object-cover border-4 border-[#f5ede3]"
        />
      </div>

      <!-- Details grid -->
      <div class="grid grid-cols-2 sm:grid-cols-3 gap-x-14 gap-y-5 flex-1">
        <div>
          <p class="text-xs font-semibold text-[#1a1a2e] mb-0.5">Company Name</p>
          <p class="text-sm text-[#555]">{{ company.name }}</p>
        </div>
        <div class="col-span-1 sm:col-span-2">
          <p class="text-xs font-semibold text-[#1a1a2e] mb-0.5">Email</p>
          <p class="text-sm text-[#555]">{{ company.email }}</p>
        </div>
        <div>
          <p class="text-xs font-semibold text-[#1a1a2e] mb-0.5">Badges</p>
          <p class="text-sm text-[#555]">{{ company.badgeCount }}</p>
        </div>
        <div>
          <p class="text-xs font-semibold text-[#1a1a2e] mb-0.5">Groups</p>
          <p class="text-sm text-[#555]">{{ company.groupCount }}</p>
        </div>
        <div>
          <p class="text-xs font-semibold text-[#1a1a2e] mb-0.5">Awardees</p>
          <p class="text-sm text-[#555]">{{ company.awardeeCount }}</p>
        </div>
      </div>
    </div>

    <!-- ── About Company card ── -->
    <div class="bg-white rounded-2xl border border-[#f0e6d8] px-6 py-5">
      <h2 class="text-sm font-extrabold text-[#1a1a2e] mb-3">About Company</h2>
      <p class="text-sm text-[#555] leading-relaxed">{{ company.about }}</p>
    </div>

    <!-- ══════════════════════════════════════
         EDIT ACCOUNT MODAL
    ══════════════════════════════════════ -->
    <Teleport to="body">
      <div
        v-if="showEditModal"
        class="fixed inset-0 z-50 flex items-center justify-center px-4"
        @click.self="showEditModal = false"
      >
        <div class="absolute inset-0 bg-black/40 backdrop-blur-sm" @click="showEditModal = false"></div>

        <div class="relative bg-white rounded-3xl shadow-2xl w-full max-w-[500px] px-8 py-8 z-10">

          <h2 class="text-xl font-extrabold text-[#1a1a2e] text-center mb-6 tracking-tight">
            Edit Account
          </h2>

          <!-- Photo picker — shows current logo + select option -->
          <label class="block w-full mb-6 cursor-pointer">
            <div
              class="w-full rounded-2xl border border-[#e8e8e8] bg-[#f8f8f8] hover:border-[#c8873a] hover:bg-[#fdf9f5] transition-all duration-200 flex items-center justify-center py-8 gap-6 group"
            >
              <!-- Current / preview logo -->
              <div class="flex-shrink-0">
                <img
                  v-if="editForm.logoPreview"
                  :src="editForm.logoPreview"
                  alt="Logo preview"
                  class="w-16 h-16 rounded-full object-cover border-4 border-white shadow-md"
                />
                <div v-else class="w-16 h-16 rounded-full bg-[#eee] border-4 border-white shadow-md flex items-center justify-center">
                  <svg class="w-7 h-7 text-[#bbb]" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"/>
                  </svg>
                </div>
              </div>

              <!-- Select photo prompt -->
              <div class="flex flex-col items-center gap-1.5">
                <svg class="w-9 h-9 text-[#c0bab5] group-hover:text-[#c8873a] transition-colors duration-200" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                  <rect x="3" y="3" width="18" height="18" rx="4" stroke-width="1.5"/>
                  <circle cx="8.5" cy="8.5" r="1.5"/>
                  <path stroke-linecap="round" stroke-linejoin="round" d="M21 15l-5-5L5 21"/>
                </svg>
                <span class="text-sm text-[#aaa] group-hover:text-[#c8873a] font-medium transition-colors duration-200">
                  Select Photo
                </span>
              </div>
            </div>
            <input type="file" accept="image/*" class="hidden" @change="handleLogoChange" />
          </label>

          <!-- First Name + Last Name -->
          <div class="grid grid-cols-2 gap-4 mb-4">
            <div class="flex flex-col gap-1.5">
              <label class="text-sm font-semibold text-[#1a1a2e]">First Name</label>
              <input
                v-model="editForm.firstName"
                type="text"
                placeholder="Placeholder"
                class="w-full bg-white border border-[#e0d5c8] rounded-lg px-4 py-3 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200"
              />
            </div>
            <div class="flex flex-col gap-1.5">
              <label class="text-sm font-semibold text-[#1a1a2e]">Last Name</label>
              <input
                v-model="editForm.lastName"
                type="text"
                placeholder="Placeholder"
                class="w-full bg-white border border-[#e0d5c8] rounded-lg px-4 py-3 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200"
              />
            </div>
          </div>

          <!-- About -->
          <div class="flex flex-col gap-1.5 mb-6">
            <label class="text-sm font-semibold text-[#1a1a2e]">About</label>
            <textarea
              v-model="editForm.about"
              placeholder="Placeholder"
              rows="6"
              class="w-full bg-white border border-[#e0d5c8] rounded-xl px-4 py-3 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200 resize-none"
            ></textarea>
          </div>

          <!-- Error -->
          <p v-if="editError" class="text-xs text-red-500 text-center mb-4">{{ editError }}</p>

          <!-- Save -->
          <button
            @click="handleSave"
            :disabled="saving"
            class="w-full bg-[#1a1a2e] hover:bg-[#2d2d4e] text-white font-bold text-sm py-4 rounded-2xl transition-all duration-200 hover:-translate-y-px disabled:opacity-60 disabled:cursor-not-allowed"
          >
            <span v-if="saving">Saving...</span>
            <span v-else>Save</span>
          </button>

        </div>
      </div>
    </Teleport>

  </div>
</template>

<script setup>
definePageMeta({ layout: 'companydashboard' })

const showEditModal = ref(false)
const saving = ref(false)
const editError = ref('')

// ── Company data — replace with real API ──
const company = ref({
  name: 'Mator Corporation',
  email: 'Magdaleneemmanual@gmail.com',
  badgeCount: 10,
  groupCount: 8,
  awardeeCount: 8,
  logo: '/images/randoms/badge.png',
  about: 'Potter ipsum wand elf parchment wingardium. In yer locomotor glasses holyhead good glory points. Kedavra prophet headmaster broomstick charm. Knut bezoar leviosa yer gillywater portrait bat it good frisbees. Turban veela and yer crookshanks. Firs\' eye splinched order great mellow umbridge. Grindlewald die tap-dancing owl plums cakes. Together sinistra he mischief stand mcgonagall witch. Hoops sorcerer\'s patronus gamp\'s sopophorous patronum feast fanged. Scabbers gillywater glass owl jinxes roaring. He doe other sorcerer\'s thieves clean law.',
})

// ── Edit form ──
const editForm = ref({
  firstName: '',
  lastName: '',
  about: '',
  logoFile: null,
  logoPreview: null,
})

const openEditModal = () => {
  // Pre-fill with current values
  const nameParts = company.value.name.split(' ')
  editForm.value.firstName = nameParts[0] || ''
  editForm.value.lastName = nameParts.slice(1).join(' ') || ''
  editForm.value.about = company.value.about
  editForm.value.logoFile = null
  editForm.value.logoPreview = company.value.logo
  editError.value = ''
  showEditModal.value = true
}

const handleLogoChange = (e) => {
  const file = e.target.files[0]
  if (!file) return
  editForm.value.logoFile = file
  editForm.value.logoPreview = URL.createObjectURL(file)
}

const handleSave = async () => {
  editError.value = ''

  if (!editForm.value.firstName.trim()) {
    editError.value = 'Please enter a company / first name.'
    return
  }

  saving.value = true
  try {
    // Add your API call here
    // e.g. await useFetch('/api/company', { method: 'PUT', body: { ...editForm.value } })
    company.value.name = `${editForm.value.firstName} ${editForm.value.lastName}`.trim()
    company.value.about = editForm.value.about
    if (editForm.value.logoPreview) company.value.logo = editForm.value.logoPreview
    showEditModal.value = false
  } catch (e) {
    editError.value = 'Something went wrong. Please try again.'
  } finally {
    saving.value = false
  }
}

useHead({ title: 'Company Account — Credeny' })
</script>
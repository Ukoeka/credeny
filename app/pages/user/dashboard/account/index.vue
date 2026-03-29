<template>
  <div>

    
    <div class="relative w-full rounded-2xl overflow-hidden mb-6 h-[200px] flex items-center justify-center">
      <img
        src="@/assets/images/backgrounds/dashboard-banner.png"
        alt=""
        class="absolute inset-0 w-full h-full object-cover"
      />
      <div class="absolute inset-0 bg-black/15"></div>

     
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
        <h1 class="text-3xl lg:text-4xl font-extrabold text-[#1a1a2e] tracking-tight">Account</h1>
        <p class="text-[#333] mt-1 text-sm">Your Credeny account</p>
      </div>
    </div>

    <!-- ── Profile info card ── -->
    <div class="bg-white rounded-2xl border border-[#f0e6d8] px-6 py-5 mb-8 flex items-center gap-6">
   
      <div class="flex-shrink-0">
        <img
          :src="profile.avatar || avatarImg"
          alt="Profile photo"
          class="w-120 h-120 rounded-full object-cover border-4 border-[#f5ede3]"
        />
      </div>

   
      <div class="grid grid-cols-2 sm:grid-cols-3 gap-x-12 gap-y-4 flex-1">
        <div>
          <p class="font-semibold text-[#1a1a2e] mb-0.5">First Name</p>
          <p class="text-[#555]">{{ profile.firstName }}</p>
        </div>
        <div>
          <p class="font-semibold text-[#1a1a2e] mb-0.5">Last Name</p>
          <p class="text-[#555]">{{ profile.lastName }}</p>
        </div>
        <div>
          <p class="font-semibold text-[#1a1a2e] mb-0.5">Email</p>
          <p class="text-[#555] break-all">{{ profile.email }}</p>
        </div>
        <div>
          <p class="font-semibold text-[#1a1a2e] mb-0.5">BAdges</p>
          <p class="text-[#555]">{{ profile.badgeCount }}</p>
        </div>
        <div>
          <p class="font-semibold text-[#1a1a2e] mb-0.5">Collections</p>
          <p class="text-[#555]">{{ profile.collectionCount }}</p>
        </div>
      </div>
    </div>

    <!-- ── Badges Collected ── -->
    <h2 class="text-lg font-extrabold text-[#1a1a2e] mb-5 tracking-tight">Badges Collected</h2>

    <div class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-5">
      <NuxtLink
        v-for="badge in badges"
        :key="badge.id"
        :to="`/user/dashboard/badge/${badge.id}`"
        class="bg-[#FFF7EE] rounded-2xl p-4 border border-[#f0e6d8] hover:shadow-md hover:-translate-y-0.5 transition-all duration-200 cursor-pointer group block"
      >
        <div class="flex justify-center mb-3">
          <img
            :src="badge.image"
            :alt="badge.title"
            class="w-[80%] h-[80%] rounded-full object-cover border-4 border-[#f5ede3] group-hover:border-[#c8873a] transition-colors duration-200"
          />
        </div>
        <div class="flex items-start justify-between gap-1">
          <div class="min-w-0">
            <h3 class="font-bold text-sm text-[#1a1a2e] truncate">{{ badge.title }}</h3>
            <p class="text-xs text-[#888] leading-relaxed mt-0.5 line-clamp-2">{{ badge.description }}</p>
            <p class="text-xs text-[#aaa] mt-2">{{ badge.date }}</p>
          </div>
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

    <!-- ══════════════════════════════════════
         EDIT ACCOUNT MODAL
    ══════════════════════════════════════ -->
    <Teleport to="body">
      <div
        v-if="showEditModal"
        class="fixed inset-0 z-50 flex items-center justify-center px-4"
        @click.self="showEditModal = false"
      >
        <!-- Backdrop -->
        <div class="absolute inset-0 bg-black/40 backdrop-blur-sm" @click="showEditModal = false"></div>

        <!-- Modal -->
        <div class="relative bg-white rounded-3xl shadow-2xl w-full max-w-[500px] px-8 py-8 z-10">

          <h2 class="text-xl font-extrabold text-[#1a1a2e] text-center mb-6 tracking-tight">
            Edit Account
          </h2>

          <!-- Photo picker -->
          <label class="block w-full mb-6 cursor-pointer">
            <div
              class="w-full rounded-2xl border-2 border-dashed border-[#e0d5c8] bg-[#faf7f3] hover:border-[#c8873a] hover:bg-[#fdf9f5] transition-all duration-200 flex flex-col items-center justify-center py-10 gap-3 group"
            >
              <!-- Preview selected photo or placeholder icon -->
              <div v-if="editForm.avatarPreview" class="relative">
                <img
                  :src="editForm.avatarPreview"
                  alt="Preview"
                  class="w-120 h-120 rounded-full object-cover border-4 border-white shadow-md"
                />
                <div class="absolute -bottom-1 -right-1 w-6 h-6 rounded-full bg-[#c8873a] flex items-center justify-center">
                  <svg class="w-3 h-3 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M15.232 5.232l3.536 3.536M9 13l6.586-6.586a2 2 0 112.828 2.828L11.828 15.828a2 2 0 01-1.414.586H8v-2.414a2 2 0 01.586-1.414z"/>
                  </svg>
                </div>
              </div>
              <div v-else class="flex flex-col items-center gap-2">
                <svg class="w-10 h-10 text-[#c8c0b5] group-hover:text-[#c8873a] transition-colors duration-200" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
                  <rect x="3" y="3" width="18" height="18" rx="4" stroke-width="1.5"/>
                  <circle cx="8.5" cy="8.5" r="1.5"/>
                  <path stroke-linecap="round" stroke-linejoin="round" d="M21 15l-5-5L5 21"/>
                </svg>
                <span class="text-sm text-[#aaa] group-hover:text-[#c8873a] transition-colors duration-200 font-medium">
                  Select Photo
                </span>
              </div>
            </div>
            <input
              type="file"
              accept="image/*"
              class="hidden"
              @change="handleAvatarChange"
            />
          </label>

          <!-- Name fields -->
          <div class="grid grid-cols-2 gap-4 mb-6">
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
import avatarImg from '@/assets/images/randoms/white-man.png'
definePageMeta({ layout: 'dashboard' })

const showEditModal = ref(false)
const saving = ref(false)
const editError = ref('')

// ── Profile data ──
const profile = ref({
  firstName: 'Mathew',
  lastName: 'Key',
  email: 'Magdaleneemmanual@gmail.com',
  badgeCount: 10,
  collectionCount: 8,
  avatar: avatarImg,
})

// ── Edit form state ──
const editForm = ref({
  firstName: '',
  lastName: '',
  avatarFile: null,
  avatarPreview: null,
})

const openEditModal = () => {
  editForm.value.firstName = profile.value.firstName
  editForm.value.lastName = profile.value.lastName
  editForm.value.avatarFile = null
  editForm.value.avatarPreview = profile.value.avatar
  editError.value = ''
  showEditModal.value = true
}

const handleAvatarChange = (e) => {
  const file = e.target.files[0]
  if (!file) return
  editForm.value.avatarFile = file
  editForm.value.avatarPreview = URL.createObjectURL(file)
}

const handleSave = async () => {
  editError.value = ''
  if (!editForm.value.firstName.trim() || !editForm.value.lastName.trim()) {
    editError.value = 'Please fill in both name fields.'
    return
  }

  saving.value = true
  try {
    // Add your API call here
    // e.g. await useFetch('/api/profile', { method: 'PUT', body: { firstName, lastName, avatar } })
    profile.value.firstName = editForm.value.firstName
    profile.value.lastName = editForm.value.lastName
    if (editForm.value.avatarPreview) {
      profile.value.avatar = editForm.value.avatarPreview
    }
    showEditModal.value = false
  } catch (e) {
    editError.value = 'Something went wrong. Please try again.'
  } finally {
    saving.value = false
  }
}

const openMenu = (id) => {
  console.log('Open menu for badge:', id)
}

// ── Badges data — replace with real API ──
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

useHead({ title: 'Account — Credeny' })
</script>
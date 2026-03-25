<template>
  <div class="relative min-h-screen pt-5 w-full flex flex-col overflow-hidden">
    <img
      src="@/assets/images/backgrounds/userdash-bg.png"
      alt=""
      class="absolute inset-0 w-full h-full object-cover"
    />

    <!-- Logo -->
    <div class="relative z-10 mt-5 p-6">
      <NuxtLink to="/" class="flex flex-col items-center w-fit gap-1">
        <img src="@/assets/images/logo/logo.png" alt="Credeny Logo" />
      </NuxtLink>
    </div>

    <!-- Centered card -->
    <div class="relative w-full z-10 flex-1 flex items-center justify-center px-4 pb-10">
      <div
        class="w-full sm:w-[80%] md:w-[60%] lg:w-[45%] xl:w-[36%]
               bg-[#f5ede3] rounded-2xl
               px-5 sm:px-8 lg:px-10
               py-8 sm:py-10
               shadow-2xl
               transition-all duration-300"
      >

        <!-- Reset Password form ── -->
        <template v-if="resetSuccess">
          <h1 class="text-xl sm:text-2xl font-extrabold text-[#1a1a2e] text-center mb-3 tracking-tight">
            Reset Password
          </h1>
          <p class="text-sm text-[#888] text-center mb-8">
            Choose a new password for your account
          </p>

          <form @submit.prevent="handleReset" class="space-y-4 sm:space-y-5">

            <!-- New Password -->
            <div class="flex flex-col gap-1.5">
              <label class="text-xs font-semibold text-[#1a1a2e]">Enter New Password</label>
              <div class="relative">
                <input
                  v-model="form.password"
                  :type="showPassword ? 'text' : 'password'"
                  placeholder="Placeholder"
                  class="w-full bg-white border border-[#e0d5c8] rounded-lg px-3.5 py-3 sm:py-4 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200 pr-10"
                />
                <button
                  type="button"
                  class="absolute right-3 top-1/2 -translate-y-1/2 text-[#aaa] hover:text-[#666] transition-colors duration-200"
                  @click="showPassword = !showPassword"
                >
                  <svg v-if="!showPassword" class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"/>
                    <path stroke-linecap="round" stroke-linejoin="round" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"/>
                  </svg>
                  <svg v-else class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M13.875 18.825A10.05 10.05 0 0112 19c-4.478 0-8.268-2.943-9.543-7a9.97 9.97 0 011.563-3.029m5.858.908a3 3 0 114.243 4.243M9.878 9.878l4.242 4.242M9.88 9.88l-3.29-3.29m7.532 7.532l3.29 3.29M3 3l3.59 3.59m0 0A9.953 9.953 0 0112 5c4.478 0 8.268 2.943 9.543 7a10.025 10.025 0 01-4.132 5.411m0 0L21 21"/>
                  </svg>
                </button>
              </div>
            </div>

            <!-- Confirm New Password -->
            <div class="flex flex-col gap-1.5">
              <label class="text-xs font-semibold text-[#1a1a2e]">Confirm New Password</label>
              <div class="relative">
                <input
                  v-model="form.confirmPassword"
                  :type="showConfirm ? 'text' : 'password'"
                  placeholder="Placeholder"
                  class="w-full bg-white border border-[#e0d5c8] rounded-lg px-3.5 py-3 sm:py-4 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200 pr-10"
                />
                <button
                  type="button"
                  class="absolute right-3 top-1/2 -translate-y-1/2 text-[#aaa] hover:text-[#666] transition-colors duration-200"
                  @click="showConfirm = !showConfirm"
                >
                  <svg v-if="!showConfirm" class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"/>
                    <path stroke-linecap="round" stroke-linejoin="round" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"/>
                  </svg>
                  <svg v-else class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M13.875 18.825A10.05 10.05 0 0112 19c-4.478 0-8.268-2.943-9.543-7a9.97 9.97 0 011.563-3.029m5.858.908a3 3 0 114.243 4.243M9.878 9.878l4.242 4.242M9.88 9.88l-3.29-3.29m7.532 7.532l3.29 3.29M3 3l3.59 3.59m0 0A9.953 9.953 0 0112 5c4.478 0 8.268 2.943 9.543 7a10.025 10.025 0 01-4.132 5.411m0 0L21 21"/>
                  </svg>
                </button>
              </div>
            </div>

            <!-- Error -->
            <p v-if="errorMsg" class="text-xs text-red-500 text-center">{{ errorMsg }}</p>

            <!-- Reset Password -->
            <button
              type="submit"
              :disabled="loading"
              class="w-full bg-[#1a1a2e] hover:bg-[#2d2d4e] text-white font-bold text-sm py-3.5 sm:py-4 rounded-xl transition-all duration-200 hover:-translate-y-px disabled:opacity-60 disabled:cursor-not-allowed"
            >
              <span v-if="loading">Resetting...</span>
              <span v-else>Reset Password</span>
            </button>

            <!-- Back to Login -->
            <NuxtLink
              to="/login"
              class="w-full flex items-center justify-center font-semibold text-sm text-[#1a1a2e] py-3.5 sm:py-4 rounded-xl border border-[#1a1a2e]/20 hover:bg-[#1a1a2e]/5 transition-all duration-200"
            >
              Back to Login
            </NuxtLink>

          </form>
        </template>

        <!-- ── Success state ── -->
        <template v-else>
          <h1 class="text-xl sm:text-2xl font-extrabold text-[#1a1a2e] text-center mb-8 tracking-tight">
            Password Reset Success
          </h1>

          <!-- Green tick circle -->
          <div class="flex justify-center pt mb-10">
            <div class="w-16 h-16 rounded-full border-2 border-green-400 flex items-center justify-center">
              <svg class="w-8 h-8 text-green-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7"/>
              </svg>
            </div>
          </div>

          <NuxtLink
            to="/login"
            class="w-full flex items-center justify-center bg-[#1a1a2e] hover:bg-[#2d2d4e] text-white font-bold text-sm py-3.5 sm:py-4 rounded-xl transition-all duration-200 hover:-translate-y-px"
          >
            Login
          </NuxtLink>
        </template>

      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

definePageMeta({ layout: false })

const form = ref({
  password: '',
  confirmPassword: '',
})

const loading = ref(false)
const errorMsg = ref('')
const showPassword = ref(false)
const showConfirm = ref(false)
const resetSuccess = ref(false)

const handleReset = async () => {
  errorMsg.value = ''

  if (!form.value.password || !form.value.confirmPassword) {
    errorMsg.value = 'Please fill in both fields.'
    return
  }
  if (form.value.password !== form.value.confirmPassword) {
    errorMsg.value = 'Passwords do not match.'
    return
  }
  if (form.value.password.length < 8) {
    errorMsg.value = 'Password must be at least 8 characters.'
    return
  }

  loading.value = true
  try {
    //  useFetch('/api/auth/reset-password', { method: 'POST', body: { password: form.value.password, token: route.query.token } })
    resetSuccess.value = true
  } catch (e) {
    errorMsg.value = 'Something went wrong. Please try again.'
  } finally {
    loading.value = false
  }
}

useHead({ title: 'Reset Password — Credeny' })
</script>
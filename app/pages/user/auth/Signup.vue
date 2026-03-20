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
        class="w-full sm:w-[90%] md:w-[75%] lg:w-[55%] xl:w-[45%]
               bg-[#f5ede3] rounded-2xl
               px-5 sm:px-8 lg:px-10
               py-8 sm:py-10
               shadow-2xl"
      >

        <h1 class="text-xl sm:text-2xl font-extrabold text-[#1a1a2e] text-center mb-6 sm:mb-8 tracking-tight">
          Sign Up
        </h1>

        <form @submit.prevent="handleSignup" class="space-y-4 sm:space-y-5">

          <!-- Row 1: Username + Email — stacked on mobile, side-by-side on sm+ -->
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div class="flex flex-col gap-1.5">
              <label class="text-xs font-semibold text-[#1a1a2e]">User Name</label>
              <input
                v-model="form.username"
                type="text"
                placeholder="Placeholder"
                class="w-full bg-white border border-[#e0d5c8] rounded-lg px-3.5 py-3 sm:py-4 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200"
              />
            </div>
            <div class="flex flex-col gap-1.5">
              <label class="text-xs font-semibold text-[#1a1a2e]">Email</label>
              <input
                v-model="form.email"
                type="email"
                placeholder="Placeholder"
                class="w-full bg-white border border-[#e0d5c8] rounded-lg px-3.5 py-3 sm:py-4 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200"
              />
            </div>
          </div>

          <!-- Row 2: Password + Confirm — stacked on mobile, side-by-side on sm+ -->
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div class="flex flex-col gap-1.5">
              <label class="text-xs font-semibold text-[#1a1a2e]">Password</label>
              <input
                v-model="form.password"
                type="password"
                placeholder="Placeholder"
                class="w-full bg-white border border-[#e0d5c8] rounded-lg px-3.5 py-3 sm:py-4 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200"
              />
            </div>
            <div class="flex flex-col gap-1.5">
              <label class="text-xs font-semibold text-[#1a1a2e]">Confirm Password</label>
              <input
                v-model="form.confirmPassword"
                type="password"
                placeholder="Placeholder"
                class="w-full bg-white border border-[#e0d5c8] rounded-lg px-3.5 py-3 sm:py-4 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200"
              />
            </div>
          </div>

          <!-- Row 3: Account Type — full width -->
          <div class="flex flex-col gap-1.5">
            <label class="text-xs font-semibold text-[#1a1a2e]">Account Type</label>
            <div class="relative">
              <select
                v-model="form.accountType"
                class="w-full appearance-none bg-white border border-[#e0d5c8] rounded-lg px-3.5 py-3 sm:py-4 text-sm text-[#333] focus:outline-none focus:border-[#c8873a] transition-colors duration-200 pr-9 cursor-pointer"
              >
                <option value="user">User Account</option>
                <option value="organization">Organization Account</option>
                <option value="issuer">Issuer Account</option>
              </select>
              <svg
                class="absolute right-3 top-1/2 -translate-y-1/2 w-4 h-4 text-[#aaa] pointer-events-none"
                fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"
              >
                <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7"/>
              </svg>
            </div>
          </div>

          <!-- Error message -->
          <p v-if="errorMsg" class="text-xs text-red-500 text-center">{{ errorMsg }}</p>

          <!-- Submit -->
          <button
            type="submit"
            :disabled="loading"
            class="w-full bg-[#1a1a2e] hover:bg-[#2d2d4e] text-white font-bold text-sm py-3.5 sm:py-4 rounded-xl transition-all duration-200 hover:-translate-y-px disabled:opacity-60 disabled:cursor-not-allowed"
          >
            <span v-if="loading">Creating account...</span>
            <span v-else>Sign Up</span>
          </button>

          <!-- Divider -->
          <div class="flex items-center gap-3">
            <div class="flex-1 h-px bg-[#ddd]"></div>
            <span class="text-xs text-[#aaa]">Or</span>
            <div class="flex-1 h-px bg-[#ddd]"></div>
          </div>

          <!-- Google sign up -->
          <button
            type="button"
            @click="handleGoogleSignup"
            class="w-full flex items-center justify-center gap-3 bg-white border border-[#e0d5c8] hover:border-[#c8873a] text-[#333] font-medium text-sm py-3.5 sm:py-4 rounded-xl transition-all duration-200 hover:shadow-md"
          >
            <img src="@/assets/images/logo/google-logo.png" alt="" class="w-5 h-5 flex-shrink-0" />
            Sign up with Google
          </button>

        </form>

        <!-- Sign in link -->
        <p class="text-center text-sm text-[#888] mt-6">
          Have an account?
          <NuxtLink
            to="/user/auth/login"
            class="font-bold text-[#1a1a2e] hover:text-[#c8873a] transition-colors duration-200 ml-1"
          >
            Sign In
          </NuxtLink>
        </p>

      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

definePageMeta({ layout: false })

const form = ref({
  username: '',
  email: '',
  password: '',
  confirmPassword: '',
  accountType: 'user',
})

const loading = ref(false)
const errorMsg = ref('')

const handleSignup = async () => {
  errorMsg.value = ''

  if (!form.value.username || !form.value.email || !form.value.password) {
    errorMsg.value = 'Please fill in all required fields.'
    return
  }
  if (form.value.password !== form.value.confirmPassword) {
    errorMsg.value = 'Passwords do not match.'
    return
  }

  loading.value = true
  try {
    await navigateTo('/dashboard')
  } catch (e) {
    errorMsg.value = 'Something went wrong. Please try again.'
  } finally {
    loading.value = false
  }
}

const handleGoogleSignup = () => {
  // Add Google OAuth logic here
}

useHead({
  title: 'Sign Up — Credeny',
})
</script>
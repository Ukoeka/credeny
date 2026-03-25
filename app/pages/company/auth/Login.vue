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
        class="w-full sm:w-[90%] md:w-[75%] lg:w-[55%] xl:w-[40%]
               bg-[#f5ede3] rounded-2xl
               px-5 sm:px-8 lg:px-10
               py-8 sm:py-10
               shadow-2xl"
      >

        <h1 class="text-xl sm:text-2xl font-extrabold text-[#1a1a2e] text-center mb-6 sm:mb-8 tracking-tight">
          Login
        </h1>

        <form @submit.prevent="handleLogin" class="space-y-4 sm:space-y-5">

          <!-- Username -->
          <div class="flex flex-col gap-1.5">
            <label class="text-xs font-semibold text-[#1a1a2e]">User Name</label>
            <input
              v-model="form.username"
              type="text"
              placeholder="Enter your username"
              class="w-full bg-white border border-[#e0d5c8] rounded-lg px-3.5 py-3 sm:py-4 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200"
            />
          </div>

          <!-- Password -->
          <div class="flex flex-col gap-1.5">
            <div class="flex items-center justify-between">
              <label class="text-xs font-semibold text-[#1a1a2e]">Password</label>
              <NuxtLink
                to="/company/auth/forgotpassword"
                class="text-xs text-[#c8873a] font-medium hover:underline"
              >
                Forgot password?
              </NuxtLink>
            </div>
            <div class="relative">
              <input
                v-model="form.password"
                :type="showPassword ? 'text' : 'password'"
                placeholder="Enter your password"
                class="w-full bg-white border border-[#e0d5c8] rounded-lg px-3.5 py-3 sm:py-4 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200 pr-10"
              />
              <!-- Show/hide toggle -->
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

          <!-- Error message -->
          <p v-if="errorMsg" class="text-xs text-red-500 text-center">{{ errorMsg }}</p>

          <!-- Submit -->
          <button
            type="submit"
            :disabled="loading"
            class="w-full bg-[#1a1a2e] hover:bg-[#2d2d4e] text-white font-bold text-sm py-3.5 sm:py-4 rounded-xl transition-all duration-200 hover:-translate-y-px disabled:opacity-60 disabled:cursor-not-allowed"
          >
            <span v-if="loading">Logging in...</span>
            <span v-else>Login</span>
          </button>

          <!-- Divider -->
          <div class="flex items-center gap-3">
            <div class="flex-1 h-px bg-[#ddd]"></div>
            <span class="text-xs text-[#aaa]">Or</span>
            <div class="flex-1 h-px bg-[#ddd]"></div>
          </div>

          <!-- Google login -->
          <button
            type="button"
            @click="handleGoogleLogin"
            class="w-full flex items-center justify-center gap-3 bg-white border border-[#e0d5c8] hover:border-[#c8873a] text-[#333] font-medium text-sm py-3.5 sm:py-4 rounded-xl transition-all duration-200 hover:shadow-md"
          >
            <img src="@/assets/images/logo/google-logo.png" alt="" class="w-5 h-5 flex-shrink-0" />
            Sign in with Google
          </button>

        </form>

        <!-- Sign up link -->
        <p class="text-center text-sm text-[#888] mt-6">
          Don't have an account?
          <NuxtLink
            to="/company/auth/signup"
            class="font-bold text-[#1a1a2e] hover:text-[#c8873a] transition-colors duration-200 ml-1"
          >
            Sign Up
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
  password: '',
})

const loading = ref(false)
const errorMsg = ref('')
const showPassword = ref(false)

const handleLogin = async () => {
  errorMsg.value = ''

  if (!form.value.username || !form.value.password) {
    errorMsg.value = 'Please fill in all fields.'
    return
  }

  loading.value = true
  try {
    // Add your login logic here
    await navigateTo('/dashboard')
  } catch (e) {
    errorMsg.value = 'Invalid username or password. Please try again.'
  } finally {
    loading.value = false
  }
}

const handleGoogleLogin = () => {
  // Add Google OAuth logic here
}

useHead({
  title: 'Login — Credeny',
})
</script>
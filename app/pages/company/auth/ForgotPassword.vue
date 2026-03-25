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
               shadow-2xl"
      >
        <h1 class="text-xl sm:text-2xl font-extrabold text-[#1a1a2e] text-center mb-4 tracking-tight">
          Forgot Password
        </h1>
        <p class="text-sm text-[#666] text-center leading-relaxed mb-8">
          Enter the email you used to create your account<br />
          so we can send you instructions on<br />
          how to reset your password.
        </p>

        <form @submit.prevent="handleSend" class="space-y-4">

          <!-- Email -->
          <div class="flex flex-col gap-1.5">
            <label class="text-xs font-semibold text-[#1a1a2e]">Email</label>
            <input
              v-model="email"
              type="email"
              placeholder="Placeholder"
              class="w-full bg-white border border-[#e0d5c8] rounded-lg px-3.5 py-3 sm:py-4 text-sm text-[#333] placeholder-[#bbb] focus:outline-none focus:border-[#c8873a] transition-colors duration-200"
            />
          </div>

          <!-- Error -->
          <p v-if="errorMsg" class="text-xs text-red-500 text-center">{{ errorMsg }}</p>

          <!-- Send -->
          <button
            type="submit"
            :disabled="loading"
            class="w-full bg-[#1a1a2e] hover:bg-[#2d2d4e] text-white font-bold text-sm py-3.5 sm:py-4 rounded-xl transition-all duration-200 hover:-translate-y-px disabled:opacity-60 disabled:cursor-not-allowed"
          >
            <span v-if="loading">Sending...</span>
            <span v-else>Send</span>
          </button>

          <!-- Back to Login -->
          <NuxtLink
            to="/user/auth/login"
            class="w-full flex items-center justify-center font-semibold text-sm text-[#1a1a2e] py-3.5 sm:py-4 rounded-xl border border-[#1a1a2e]/20 hover:bg-[#1a1a2e]/5 transition-all duration-200"
          >
            Back To Login
          </NuxtLink>

        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

definePageMeta({ layout: false })

const email = ref('')
const loading = ref(false)
const errorMsg = ref('')

const handleSend = async () => {
  errorMsg.value = ''

  if (!email.value) {
    errorMsg.value = 'Please enter your email address.'
    return
  }

  loading.value = true
  try {
    // Add your forgot password logic here
    // e.g. await useFetch('/api/auth/forgot-password', { method: 'POST', body: { email: email.value } })
    await navigateTo(`/verify-email?email=${encodeURIComponent(email.value)}`)
  } catch (e) {
    errorMsg.value = 'Something went wrong. Please try again.'
  } finally {
    loading.value = false
  }
}

useHead({ title: 'Forgot Password — Credeny' })
</script>
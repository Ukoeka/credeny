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
        <h1 class="text-xl sm:text-2xl font-extrabold text-[#1a1a2e] text-center mb-5 tracking-tight">
          Verify your Email
        </h1>

        <p class="text-sm text-[#555] text-center leading-relaxed mb-2">
          We have sent a verification email to
          <span class="font-bold text-[#1a1a2e]">{{ maskedEmail }}</span>
        </p>
        <p class="text-sm text-[#888] text-center mb-8">
          Didn't receive the email? Check spam or
        </p>

        <div class="space-y-3">
          <!-- Resend Email -->
          <button
            @click="handleResend"
            :disabled="resendLoading || resendCooldown > 0"
            class="w-full bg-[#1a1a2e] hover:bg-[#2d2d4e] text-white font-bold text-sm py-3.5 sm:py-4 rounded-xl transition-all duration-200 hover:-translate-y-px disabled:opacity-60 disabled:cursor-not-allowed"
          >
            <span v-if="resendLoading">Sending...</span>
            <span v-else-if="resendCooldown > 0">Resend in {{ resendCooldown }}s</span>
            <span v-else>Resend Email</span>
          </button>

          <!-- Change Email -->
          <NuxtLink
            to="/forgot-password"
            class="w-full flex items-center justify-center font-semibold text-sm text-[#1a1a2e] py-3.5 sm:py-4 rounded-xl border border-[#1a1a2e]/20 hover:bg-[#1a1a2e]/5 transition-all duration-200"
          >
            Change Email
          </NuxtLink>
        </div>

        <!-- Success feedback -->
        <p v-if="resentMsg" class="text-xs text-green-600 text-center mt-4">{{ resentMsg }}</p>

      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onUnmounted } from 'vue'

definePageMeta({ layout: false })

const route = useRoute()

// Get email from query param — e.g. /verify-email?email=user@gmail.com
const rawEmail = computed(() => route.query.email || 'Fav*****@Gmail.com')

// Mask email: show first 3 chars + ***** + @domain
const maskedEmail = computed(() => {
  const e = rawEmail.value
  const [local, domain] = e.split('@')
  if (!domain) return e
  const visible = local.slice(0, 3)
  return `${visible}*****@${domain}`
})

const resendLoading = ref(false)
const resendCooldown = ref(0)
const resentMsg = ref('')
let cooldownTimer = null

const handleResend = async () => {
  resentMsg.value = ''
  resendLoading.value = true
  try {
    // Add your resend email logic here
    resentMsg.value = 'Verification email resent successfully!'
    // Start 30s cooldown
    resendCooldown.value = 30
    cooldownTimer = setInterval(() => {
      resendCooldown.value--
      if (resendCooldown.value <= 0) clearInterval(cooldownTimer)
    }, 1000)
  } catch (e) {
    resentMsg.value = 'Failed to resend. Please try again.'
  } finally {
    resendLoading.value = false
  }
}

onUnmounted(() => { if (cooldownTimer) clearInterval(cooldownTimer) })

useHead({ title: 'Verify Email — Credeny' })
</script>
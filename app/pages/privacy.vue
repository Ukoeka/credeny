<template>
  <SharedLayout>

    <!-- HERO -->
    <section class="pt-[120px]">
      <div class="mx-auto px-6 sm:px-10 lg:px-20 py-10">
        <div
          class="relative w-full rounded-2xl overflow-hidden min-h-[300px] sm:min-h-[400px] flex items-center justify-center text-center px-4 sm:px-6 py-12 sm:py-16 bg-cover bg-center"
          :style="{ backgroundImage: `url(${heroBg})` }"
        >
          <div class="absolute inset-0 bg-black/60"></div>

          <div class="relative z-10">
            <h1 class="text-2xl sm:text-3xl lg:text-5xl font-extrabold text-white mb-4">
              We care about your privacy
            </h1>
            <p class="text-sm sm:text-base text-white/90 leading-relaxed max-w-md mx-auto">
              We care about your privacy at Credeny.
              This Privacy Policy outlines how we collect,
              use, and safeguard your data when you use our services.
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- INTRO -->
    <section class="bg-[#f5ede3] py-12 sm:py-16">
      <div class="max-w-3xl mx-auto px-6 sm:px-10 text-center">
        <p class="text-[#444] text-base sm:text-lg leading-relaxed">
          Welcome to <span class="text-[#c8873a] font-bold">Credeny</span> where we prioritize the protection
          and privacy of your personal information. This Privacy Policy outlines how we collect, use, and
          safeguard your data when you use our services.
        </p>
      </div>
    </section>

    <!-- INFORMATION WE COLLECT -->
    <section class="bg-black text-white">
      <div class="grid grid-cols-1 lg:grid-cols-2 min-h-[70vh]">

        <!-- TEXT -->
        <div class="flex justify-center items-center px-6 sm:px-10 lg:px-20 py-12">
          <div class="max-w-lg w-full">
            <h2 class="text-2xl sm:text-3xl lg:text-5xl font-extrabold mb-6">
              Information We Collect
            </h2>

            <div class="space-y-4 text-white/80 leading-relaxed">
              <p class="text-base sm:text-lg">
                <span class="font-semibold text-white">Personal Information:</span>
                When you create an account, we may collect your name, email address, and contact details.
              </p>
              <p class="text-base sm:text-lg">
                <span class="font-semibold text-white">Credential Information:</span>
                We securely store and manage your digital credentials.
              </p>
              <p class="text-base sm:text-lg">
                <span class="font-semibold text-white">Usage Data:</span>
                We gather how you interact with our platform.
              </p>
            </div>
          </div>
        </div>

        <!-- IMAGE -->
        <div class="relative h-[250px] sm:h-[350px] lg:h-auto">
          <img
            src="@/assets/images/randoms/collect.png"
            class="absolute inset-0 w-full h-full object-cover"
          />
        </div>

      </div>
    </section>

    <!-- HOW WE USE -->
    <section class="bg-black text-white">
      <div class="grid grid-cols-1 lg:grid-cols-2 min-h-[70vh]">

        <!-- IMAGE -->
        <div class="relative h-[250px] sm:h-[350px] lg:h-auto">
          <img
            src="@/assets/images/randoms/use.png"
            class="absolute inset-0 w-full h-full object-cover"
          />
        </div>

        <!-- TEXT -->
        <div class="flex items-center justify-center px-6 sm:px-10 lg:px-20 py-12">
          <div class="max-w-lg w-full">
            <h2 class="text-2xl sm:text-3xl lg:text-5xl font-extrabold mb-6">
              How We Use This Information
            </h2>

            <div class="space-y-4 text-white/80 leading-relaxed">
              <p class="text-base sm:text-lg">
                <span class="font-semibold text-white">Personal Information:</span>
                Used to manage your account and communication.
              </p>
              <p class="text-base sm:text-lg">
                <span class="font-semibold text-white">Credential Information:</span>
                Used to display and verify your achievements.
              </p>
              <p class="text-base sm:text-lg">
                <span class="font-semibold text-white">Usage Data:</span>
                Helps us improve user experience.
              </p>
            </div>
          </div>
        </div>

      </div>
    </section>

    <!-- DATA SECURITY -->
    <section class="bg-[#f5ede3]">
      <div class="grid grid-cols-1 lg:grid-cols-2 min-h-[70vh]">

        <!-- TEXT -->
        <div class="flex items-center justify-center px-6 sm:px-10 lg:px-20 py-12">
          <div class="max-w-lg w-full">
            <h2 class="text-2xl sm:text-3xl lg:text-5xl font-extrabold text-[#1a1a2e] mb-6">
              Data Security
            </h2>

            <div class="space-y-4 text-[#555] leading-relaxed">
              <p class="text-base sm:text-lg">
                <span class="font-semibold text-[#1a1a2e]">Protection:</span>
                We implement strong security measures to protect your data.
              </p>
              <p class="text-base sm:text-lg">
                <span class="font-semibold text-[#1a1a2e]">Encryption:</span>
                Your sensitive information is encrypted.
              </p>
              <p class="text-base sm:text-lg">
                <span class="font-semibold text-[#1a1a2e]">Access Control:</span>
                Only authorized personnel can access your data.
              </p>
            </div>
          </div>
        </div>

        <!-- IMAGE -->
        <div class="relative h-[250px] sm:h-[350px] lg:h-auto">
          <img
            src="@/assets/images/randoms/data.png"
            class="absolute inset-0 w-full h-full object-cover"
          />
        </div>

      </div>
    </section>

    <!-- THIRD PARTY -->
    <section class="bg-[#f5ede3]">
      <div class="grid grid-cols-1 lg:grid-cols-2 min-h-[70vh]">

        <!-- IMAGE -->
        <div class="relative h-[250px] sm:h-[350px] lg:h-auto">
          <img
            src="@/assets/images/randoms/service.png"
            class="absolute inset-0 w-full h-full object-cover"
          />
        </div>

        <!-- TEXT -->
        <div class="flex items-center justify-center px-6 sm:px-10 lg:px-20 py-12 bg-white">
          <div class="max-w-lg w-full">
            <h2 class="text-2xl sm:text-3xl lg:text-5xl font-extrabold text-[#1a1a2e] mb-6">
              Third-Party Services
            </h2>

            <div class="space-y-4 text-[#555] leading-relaxed">
              <p class="text-base sm:text-lg">
                We may use trusted third-party services to improve functionality.
              </p>
              <p class="text-base sm:text-lg">
                These providers are required to protect your data.
              </p>
              <p class="text-base sm:text-lg">
                We do not sell or misuse your personal information.
              </p>
            </div>
          </div>
        </div>

      </div>
    </section>

    <!-- CONTACT -->
    <section class="bg-black text-white">
      <div class="grid grid-cols-1 lg:grid-cols-2 min-h-[500px]">

        <!-- TEXT -->
        <div class="flex justify-center items-center px-6 sm:px-10 lg:px-20 py-12">
          <div class="max-w-md">
            <p class="text-[#c8873a] text-sm font-bold mb-3 uppercase tracking-widest">
              We're Always In Touch
            </p>
            <h2 class="text-2xl sm:text-3xl lg:text-4xl font-extrabold mb-4">
              Contact Us
            </h2>
            <p class="text-white/70 text-sm mb-3">
              If you have any questions, feel free to reach out.
            </p>
            <p class="text-white/70 text-sm">
              Thank you for trusting Credeny.
            </p>
          </div>
        </div>

        <!-- FORM -->
        <div class="flex justify-center items-center px-6 sm:px-10 lg:px-20 py-12">
          <div class="w-full max-w-lg">
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 mb-4">
              <input v-model="form.email" type="email" placeholder="Your Email"
                class="bg-white rounded-lg px-4 py-3 text-sm text-black" />
              <input v-model="form.phone" type="tel" placeholder="Mobile Number"
                class="bg-white rounded-lg px-4 py-3 text-sm text-black" />
            </div>

            <textarea v-model="form.message" rows="5" placeholder="Your Message"
              class="w-full bg-white rounded-lg px-4 py-3 text-sm text-black mb-4"></textarea>

            <button @click="handleSubmit"
              class="w-full bg-[#c8873a] text-white font-bold py-3 rounded-lg">
              Send
            </button>
          </div>
        </div>

      </div>
    </section>

  </SharedLayout>
</template>

<script setup>
import { ref } from 'vue'
import heroBg from '@/assets/images/randoms/coffee.jpg'
import SharedLayout from '~/layouts/SharedLayout.vue'

const form = ref({
  email: '',
  phone: '',
  message: '',
})

const handleSubmit = () => {
  console.log(form.value)
}

useHead({
  title: 'Privacy Policy — Credeny',
})
</script>
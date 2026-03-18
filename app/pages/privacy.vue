<template>
  <SharedLayout>

    <!-- ═══════════════════════════════════════════
         HERO BANNER
    ═══════════════════════════════════════════ -->
    <section class="pt-[68px] ">
      <div class="mx-auto px-20 lg:px-20 py-10">
        <div
    class="relative w-full rounded-2xl overflow-hidden min-h-[300px] flex items-center justify-center text-center px-6 py-16 bg-cover bg-center bg-no-repeat"
    :style="{ backgroundImage: `url(${heroBg})` }"
  >
    <!-- your content -->
  
          <!-- Dark overlay -->
          <div class="absolute inset-0 bg-black/50"></div>

          <!-- Content -->
          <div class="relative z-10">
            <h1 class="text-3xl lg:text-4xl font-extrabold text-white mb-4 tracking-tight">
              We care about your privacy
            </h1>
            <p class="text-white text-sm lg:text-base leading-relaxed max-w-md mx-auto">
              We care about your privacy at Credeny.<br />
              This Privacy Policy outlines how we collect,<br />
              use, and safeguard your data when you use our services.
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- ═══════════════════════════════════════════
         INTRO TEXT
    ═══════════════════════════════════════════ -->
    <section class="bg-[#f5ede3] py-16">
      <div class="max-w-[860px] mx-auto px-6 lg:px-10 text-center">
        <p class="text-[#444] text-base lg:text-lg leading-relaxed">
          Welcome to <span class="text-[#c8873a] font-bold">Credeny</span> where we prioritize the protection
          and privacy of your personal <br> information. This Privacy Policy outlines how we collect, use, and
          safeguard your data <br> when you use our services.
        </p>
      </div>
    </section>

    <!-- ═══════════════════════════════════════════
         INFORMATION WE COLLECT
    ═══════════════════════════════════════════ -->
    <section class="bg-black text-white justify-center flex w-full">
      <div class="grid lg:grid-cols-2 min-h-[600px]">

        <!-- Left: text -->
        <div class="flex items-center px-10 lg:px-20 py-16">
          <div class="max-w-md">
            <h2 class="text-3xl lg:text-5xl font-extrabold mb-6 tracking-tight">
              Information We Collect
            </h2>
            <div class="space-y-4 text-white/75 text-sm leading-relaxed">
              <p>
                <span class="font-semibold text-white">Personal Information:</span>
                When you create an account, we may collect information such as your name, email address, and contact details.
              </p>
              <p>
                <span class="font-semibold text-white">Credential Information:</span>
                We securely store and manage your digital credentials, including certificates, badges, and other achievements.
              </p>
              <p>
                <span class="font-semibold text-white">Usage Data:</span>
                We gather information about how you interact with our site, such as your browsing activity and preferences.
              </p>
            </div>
          </div>
        </div>

        <!-- Right: image — replace src with your actual image -->
        <div class="relative min-h-[500px] lg:min-h-0">
          <img
            src="@/assets/images/randoms/collect.png"
            alt="People collaborating"
            class="absolute inset-0 w-full h-full object-cover"
          />
        </div>
      </div>
    </section>

    <!-- ═══════════════════════════════════════════
         HOW WE USE THIS INFORMATION
    ═══════════════════════════════════════════ -->
    <section class="bg-[#1a1a2e] text-white">
      <div class="grid lg:grid-cols-2 min-h-[420px]">

        <!-- Left: image — replace src with your actual image -->
        <div class="relative min-h-[360px] lg:min-h-0">
          <img
            src="@/assets/images/randoms/use.png"
            alt="Team discussing"
            class="absolute inset-0 w-full h-full object-cover"
          />
        </div>

        <!-- Right: text -->
        <div class="flex items-center px-10 lg:px-20 py-16">
          <div class="max-w-md">
            <h2 class="text-2xl lg:text-3xl font-extrabold mb-6 tracking-tight">
              How We Use This Information
            </h2>
            <div class="space-y-4 text-white/75 text-sm leading-relaxed">
              <p>
                <span class="font-semibold text-white">Personal Information:</span>
                When you create an account, we may collect information such as your name, email address, and contact details.
              </p>
              <p>
                <span class="font-semibold text-white">Credential Information:</span>
                We securely store and manage your digital credentials, including certificates, badges, and other achievements.
              </p>
              <p>
                <span class="font-semibold text-white">Usage Data:</span>
                We gather information about how you interact with our site, such as your browsing activity and preferences.
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ═══════════════════════════════════════════
         DATA SECURITY
    ═══════════════════════════════════════════ -->
    <section class="bg-[#f5ede3]">
      <div class="grid lg:grid-cols-2 min-h-[420px]">

        <!-- Left: text -->
        <div class="flex items-center px-10 lg:px-20 py-16">
          <div class="max-w-md">
            <h2 class="text-2xl lg:text-3xl font-extrabold text-[#1a1a2e] mb-6 tracking-tight">
              Data Security
            </h2>
            <div class="space-y-4 text-[#555] text-sm leading-relaxed">
              <p>
                <span class="font-semibold text-[#1a1a2e]">Personal Information:</span>
                When you create an account, we may collect information such as your name, email address, and contact details.
              </p>
              <p>
                <span class="font-semibold text-[#1a1a2e]">Credential Information:</span>
                We securely store and manage your digital credentials, including certificates, badges, and other achievements.
              </p>
              <p>
                <span class="font-semibold text-[#1a1a2e]">Usage Data:</span>
                We gather information about how you interact with our site, such as your browsing activity and preferences.
              </p>
            </div>
          </div>
        </div>

        <!-- Right: image — replace src with your actual image -->
        <div class="relative min-h-[360px] lg:min-h-0 bg-[#e8e8e8]">
          <img
            src="@/assets/images/randoms/data.png"
            alt="Data security illustration"
            class="absolute inset-0 w-full h-full object-cover"
          />
        </div>
      </div>
    </section>

    <!-- ═══════════════════════════════════════════
         THIRD-PARTY SERVICES
    ═══════════════════════════════════════════ -->
    <section class="bg-[#f5ede3]">
      <div class="grid lg:grid-cols-2 min-h-[380px]">

        <!-- Left: image — replace src with your actual image -->
        <div class="relative min-h-[340px] lg:min-h-0">
          <img
            src="@/assets/images/randoms/service.png"
            alt="Business professionals"
            class="absolute inset-0 w-full h-full object-cover"
          />
        </div>

        <!-- Right: text -->
        <div class="flex items-center px-10 lg:px-20 py-16 bg-white">
          <div class="max-w-md">
            <h2 class="text-2xl lg:text-3xl font-extrabold text-[#1a1a2e] mb-6 tracking-tight">
              Third-Party Services
            </h2>
            <div class="space-y-4 text-[#555] text-sm leading-relaxed">
              <p>
                <span class="font-semibold text-[#1a1a2e]">Personal Information:</span>
                When you create an account, we may collect information such as your name, email address, and contact details.
              </p>
              <p>
                <span class="font-semibold text-[#1a1a2e]">Credential Information:</span>
                We securely store and manage your digital credentials, including certificates, badges, and other achievements.
              </p>
              <p>
                <span class="font-semibold text-white">Usage Data:</span>
                We gather information about how you interact with our site, such as your browsing activity and preferences.
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ═══════════════════════════════════════════
         CONTACT US
    ═══════════════════════════════════════════ -->
    <section id="contact" class="bg-[#1a1a2e] text-white">
      <div class="grid lg:grid-cols-2 min-h-[420px]">

        <!-- Left: text -->
        <div class="flex items-center px-10 lg:px-20 py-16">
          <div class="max-w-sm">
            <p class="text-[#c8873a] font-bold text-sm uppercase tracking-widest mb-3">
              We're Always In Touch
            </p>
            <h2 class="text-3xl lg:text-4xl font-extrabold mb-5 tracking-tight">
              Contact Us
            </h2>
            <p class="text-white/70 text-sm leading-relaxed mb-3">
              If you have any questions or concerns about our Privacy Policy or our data practices, please contact us.
            </p>
            <p class="text-white/70 text-sm leading-relaxed">
              Thank you for trusting Credeny with your digital credentials!
            </p>
          </div>
        </div>

        <!-- Right: contact form -->
        <div class="flex items-center px-10 lg:px-20 py-16">
          <div class="w-full max-w-lg">
            <div class="grid grid-cols-2 gap-4 mb-4">
              <input
                v-model="form.email"
                type="email"
                placeholder="Your Email"
                class="col-span-1 bg-transparent border border-white/20 rounded-lg px-4 py-3 text-sm text-white placeholder-white/40 focus:outline-none focus:border-[#c8873a] transition-colors duration-200"
              />
              <input
                v-model="form.phone"
                type="tel"
                placeholder="Mobile Number"
                class="col-span-1 bg-transparent border border-white/20 rounded-lg px-4 py-3 text-sm text-white placeholder-white/40 focus:outline-none focus:border-[#c8873a] transition-colors duration-200"
              />
            </div>
            <textarea
              v-model="form.message"
              placeholder="Your Message"
              rows="5"
              class="w-full bg-transparent border border-white/20 rounded-lg px-4 py-3 text-sm text-white placeholder-white/40 focus:outline-none focus:border-[#c8873a] transition-colors duration-200 resize-none mb-4"
            ></textarea>
            <button
              @click="handleSubmit"
              class="w-full bg-[#c8873a] hover:bg-[#b5762f] text-white font-bold text-sm py-3.5 rounded-lg transition-all duration-200 hover:-translate-y-px tracking-wide"
            >
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

const form = ref({
  email: '',
  phone: '',
  message: '',
})

const handleSubmit = () => {
  // Handle form submission
  console.log('Form submitted:', form.value)
}

useHead({
  title: 'Privacy Policy — Credeny',
  meta: [
    { name: 'description', content: 'Learn how Credeny collects, uses, and safeguards your personal data and digital credentials.' },
  ],
})
</script>
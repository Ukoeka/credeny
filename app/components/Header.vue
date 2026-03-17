<template>
  <header
    class="fixed top-0 left-0 w-full z-50 bg-[#f5ede3] transition-all duration-300"
    :class="isScrolled ? 'shadow-[0_2px_24px_rgba(26,26,46,0.10)] backdrop-blur-md' : ''"
  >
    <!-- Main bar -->
    <div class="max-w-[1200px] mx-auto h-[68px] px-6 lg:px-10 flex items-center gap-6">

      <!-- Logo -->
      <NuxtLink to="/" class="flex items-center gap-2 no-underline flex-shrink-0">
        <svg width="36" height="36" viewBox="0 0 36 36" fill="none" xmlns="http://www.w3.org/2000/svg">
          <circle cx="18" cy="18" r="17" stroke="#1a1a2e" stroke-width="2"/>
          <path d="M11 18C11 14.134 14.134 11 18 11C19.933 11 21.683 11.783 22.95 13.05" stroke="#c8873a" stroke-width="2.2" stroke-linecap="round"/>
          <path d="M25 18C25 21.866 21.866 25 18 25C16.067 25 14.317 24.217 13.05 22.95" stroke="#1a1a2e" stroke-width="2.2" stroke-linecap="round"/>
          <circle cx="18" cy="18" r="3" fill="#c8873a"/>
        </svg>
        <span class="font-bold text-[0.95rem] tracking-[0.12em] text-[#1a1a2e]">CREDENY</span>
      </NuxtLink>

      <!-- Desktop Nav -->
      <nav class="hidden md:flex items-center gap-0.5 ml-auto">
        <NuxtLink
          v-for="item in navItems"
          :key="item.label"
          :to="item.href"
          class="text-sm font-medium text-[#1a1a2e] no-underline px-3 py-1.5 rounded-md transition-all duration-200 hover:text-[#c8873a] hover:bg-[#c8873a]/10"
          active-class="!text-[#c8873a] bg-[#c8873a]/10"
        >
          {{ item.label }}
        </NuxtLink>
      </nav>

      <!-- Desktop CTAs -->
      <div class="hidden md:flex items-center gap-3 flex-shrink-0">
        <NuxtLink
          to="/login"
          class="text-sm font-semibold text-[#1a1a2e] no-underline px-4 py-[0.45rem] border-[1.5px] border-[#1a1a2e] rounded-md transition-all duration-200 hover:bg-[#1a1a2e] hover:text-white"
        >
          Login
        </NuxtLink>
        <NuxtLink
          to="/signup"
          class="text-sm font-semibold text-white no-underline px-4 py-[0.45rem] bg-[#1a1a2e] border-[1.5px] border-[#1a1a2e] rounded-md transition-all duration-200 hover:bg-[#2d2d4e] hover:-translate-y-px"
        >
          Sign up
        </NuxtLink>
      </div>

      <!-- Hamburger — nth-child transforms need minimal scoped style -->
      <button
        class="md:hidden ml-auto flex flex-col justify-center gap-[5px] w-9 h-9 bg-transparent border-none cursor-pointer p-1 flex-shrink-0"
        :class="{ 'is-open': mobileMenuOpen }"
        @click="mobileMenuOpen = !mobileMenuOpen"
        aria-label="Toggle menu"
      >
        <span class="hb-bar block h-0.5 w-full bg-[#1a1a2e] rounded-sm transition-all duration-300 origin-center"></span>
        <span class="hb-bar block h-0.5 w-full bg-[#1a1a2e] rounded-sm transition-all duration-300 origin-center"></span>
        <span class="hb-bar block h-0.5 w-full bg-[#1a1a2e] rounded-sm transition-all duration-300 origin-center"></span>
      </button>
    </div>

    <!-- Mobile dropdown -->
    <div
      class="md:hidden overflow-hidden transition-all duration-300 ease-in-out bg-[#f5ede3]"
      :class="mobileMenuOpen ? 'max-h-[400px] border-t border-[#1a1a2e]/10' : 'max-h-0'"
    >
      <nav class="flex flex-col gap-0.5 px-6 pt-3 pb-5">
        <NuxtLink
          v-for="item in navItems"
          :key="item.label"
          :to="item.href"
          class="text-base font-medium text-[#1a1a2e] no-underline px-3 py-2.5 rounded-md transition-all duration-200 hover:text-[#c8873a] hover:bg-[#c8873a]/8"
          @click="mobileMenuOpen = false"
        >
          {{ item.label }}
        </NuxtLink>
        <div class="flex flex-col gap-2 mt-4 pt-4 border-t border-[#1a1a2e]/10">
          <NuxtLink
            to="/login"
            class="text-sm font-semibold text-[#1a1a2e] no-underline text-center px-4 py-2.5 border-[1.5px] border-[#1a1a2e] rounded-md transition-all duration-200 hover:bg-[#1a1a2e] hover:text-white"
            @click="mobileMenuOpen = false"
          >
            Login
          </NuxtLink>
          <NuxtLink
            to="/signup"
            class="text-sm font-semibold text-white no-underline text-center px-4 py-2.5 bg-[#1a1a2e] rounded-md transition-all duration-200 hover:bg-[#2d2d4e]"
            @click="mobileMenuOpen = false"
          >
            Sign up
          </NuxtLink>
        </div>
      </nav>
    </div>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const mobileMenuOpen = ref(false)

const navItems = [
  { label: 'Home', href: '/' },
  { label: 'Features', href: '/#features' },
  { label: 'Pricing', href: '/#pricing' },
  { label: 'Testimonials', href: '/#testimonials' },
  { label: 'Contact', href: '/#contact' },
]

const handleScroll = () => { isScrolled.value = window.scrollY > 20 }
onMounted(() => window.addEventListener('scroll', handleScroll))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<style scoped>
/* nth-child transforms cannot be expressed in Tailwind — minimal necessary styles only */
.is-open .hb-bar:nth-child(1) { transform: translateY(7px) rotate(45deg); }
.is-open .hb-bar:nth-child(2) { opacity: 0; transform: scaleX(0); }
.is-open .hb-bar:nth-child(3) { transform: translateY(-7px) rotate(-45deg); }
</style>
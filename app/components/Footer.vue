<template>
  <footer>

    <!-- ── CTA Band ── -->
    <section class="bg-[#f9f3ec] py-16 px-6 lg:px-10">
      <div class="max-w-[1100px] mx-auto flex flex-col md:flex-row items-center justify-between gap-12">

        <!-- Text side -->
        <div class="text-center md:text-left">
          <h2 class="text-[clamp(1.6rem,3vw,2.2rem)] font-extrabold text-[#1a1a2e] leading-tight tracking-tight mb-3">
            Ready To Get Started?
          </h2>
          <p class="text-sm text-[#555] leading-relaxed mb-8">
            Join Thousands Of Satisfied Users And Start<br class="hidden sm:block" />
            Issuing Digital Credentials Today.
          </p>
          <div class="flex flex-wrap gap-3 justify-center md:justify-start">
            <NuxtLink
              to="/signup"
              class="inline-block text-sm font-bold text-white no-underline px-6 py-2.5 bg-[#1a1a2e] border-2 border-[#1a1a2e] rounded-lg transition-all duration-200 hover:bg-[#2d2d4e] hover:-translate-y-px tracking-wide"
            >
              Sign Up
            </NuxtLink>
            <NuxtLink
              to="/demo"
              class="inline-block text-sm font-bold text-[#1a1a2e] no-underline px-6 py-2.5 bg-transparent border-2 border-[#1a1a2e] rounded-lg transition-all duration-200 hover:bg-[#1a1a2e] hover:text-white tracking-wide"
            >
              Request A Demo
            </NuxtLink>
          </div>
        </div>

        <!-- Visual: dots + avatar cluster + dots -->
        <div class="flex flex-col items-center gap-5 flex-shrink-0" aria-hidden="true">
          <!-- Top dot grid -->
          <div class="grid grid-cols-6 gap-1.5">
            <span
              v-for="i in 12"
              :key="'td'+i"
              class="w-[5px] h-[5px] rounded-full bg-[#c8873a] opacity-40"
            ></span>
          </div>

          <!-- Avatar cluster -->
          <div class="flex items-center">
            <div
              v-for="(av, i) in avatars"
              :key="i"
              class="w-[52px] h-[52px] rounded-full border-[3px] border-[#f9f3ec] bg-[#1a1a2e] flex items-center justify-center overflow-hidden flex-shrink-0"
              :class="i > 0 ? '-ml-3' : ''"
              :style="`z-index: ${5 - i}`"
            >
              <img v-if="av.src" :src="av.src" :alt="'User ' + (i + 1)" class="w-full h-full object-cover" />
              <span v-else class="text-xs font-bold text-white tracking-wide">{{ av.initials }}</span>
            </div>
          </div>

          <!-- Bottom dot grid -->
          <div class="grid grid-cols-4 gap-1.5">
            <span
              v-for="i in 12"
              :key="'bd'+i"
              class="w-[5px] h-[5px] rounded-full bg-[#c8873a] opacity-40"
            ></span>
          </div>
        </div>
      </div>
    </section>

    <!-- ── Dark footer ── -->
    <div class="bg-[#1a1a2e] px-6 lg:px-10 pt-10 pb-6">
      <div class="max-w-[1100px] mx-auto">

        <!-- Logo + social  |  Nav links -->
        <div class="flex flex-col md:flex-row items-start md:items-center justify-between gap-8 pb-8 border-b border-white/10 flex-wrap">

          <!-- Brand -->
          <div>
            <NuxtLink to="/" class="flex items-center gap-2 no-underline mb-5">
              <svg width="32" height="32" viewBox="0 0 36 36" fill="none" xmlns="http://www.w3.org/2000/svg">
                <circle cx="18" cy="18" r="17" stroke="#fff" stroke-width="2"/>
                <path d="M11 18C11 14.134 14.134 11 18 11C19.933 11 21.683 11.783 22.95 13.05" stroke="#c8873a" stroke-width="2.2" stroke-linecap="round"/>
                <path d="M25 18C25 21.866 21.866 25 18 25C16.067 25 14.317 24.217 13.05 22.95" stroke="#fff" stroke-width="2.2" stroke-linecap="round"/>
                <circle cx="18" cy="18" r="3" fill="#c8873a"/>
              </svg>
              <span class="font-bold text-[0.95rem] tracking-[0.12em] text-white">CREDENY</span>
            </NuxtLink>

            <!-- Social icons -->
            <div class="flex items-center gap-2">
              <a
                v-for="social in socials"
                :key="social.label"
                :href="social.href"
                :aria-label="social.label"
                class="flex items-center justify-center w-9 h-9 rounded-lg bg-white/8 text-white/60 transition-all duration-200 hover:bg-[#c8873a] hover:text-white"
              >
                <svg width="17" height="17" viewBox="0 0 24 24" fill="currentColor" v-html="social.path"></svg>
              </a>
            </div>
          </div>

          <!-- Nav links -->
          <nav class="flex flex-wrap gap-x-10 gap-y-3">
            <NuxtLink
              v-for="link in footerLinks"
              :key="link.label"
              :to="link.href"
              class="text-sm font-medium text-white/55 no-underline transition-colors duration-200 hover:text-white"
            >
              {{ link.label }}
            </NuxtLink>
          </nav>
        </div>

        <!-- Bottom bar -->
        <div class="flex flex-col sm:flex-row items-start sm:items-center justify-between gap-3 pt-5 flex-wrap">
          <span class="text-xs text-white/35">© {{ year }} Credeny. All rights reserved.</span>
          <div class="flex items-center gap-5">
            <NuxtLink
              v-for="leg in legalLinks"
              :key="leg.label"
              :to="leg.href"
              class="text-xs text-white/45 no-underline transition-colors duration-200 hover:text-white"
            >
              {{ leg.label }}
            </NuxtLink>
          </div>
        </div>

      </div>
    </div>
  </footer>
</template>

<script setup>
import { computed } from 'vue'

const year = computed(() => new Date().getFullYear())

const footerLinks = [
  { label: 'Link 1', href: '#' },
  { label: 'Link 2', href: '#' },
  { label: 'Link 3', href: '#' },
  { label: 'Link 4', href: '#' },
  { label: 'Link 5', href: '#' },
]

const legalLinks = [
  { label: 'Privacy Policy', href: '/privacy' },
  { label: 'Terms of Service', href: '/terms' },
  { label: 'Cookies Settings', href: '/cookies' },
]

// Replace src values with real paths e.g. '/images/avatar-1.jpg'
const avatars = [
  { src: '', initials: 'AM' },
  { src: '', initials: 'BK' },
  { src: '', initials: 'CL' },
  { src: '', initials: 'DJ' },
  { src: '', initials: 'EO' },
]

// SVG path inner HTML for each social icon
const socials = [
  {
    label: 'Twitter / X',
    href: '#',
    path: '<path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-4.714-6.231-5.401 6.231H2.748l7.73-8.835L1.254 2.25H8.08l4.253 5.622zm-1.161 17.52h1.833L7.084 4.126H5.117z"/>',
  },
  {
    label: 'LinkedIn',
    href: '#',
    path: '<path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>',
  },
  {
    label: 'Instagram',
    href: '#',
    path: '<path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838a6.162 6.162 0 100 12.324 6.162 6.162 0 000-12.324zM12 16a4 4 0 110-8 4 4 0 010 8zm6.406-11.845a1.44 1.44 0 100 2.881 1.44 1.44 0 000-2.881z"/>',
  },
  {
    label: 'Facebook',
    href: '#',
    path: '<path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/>',
  },
]
</script>
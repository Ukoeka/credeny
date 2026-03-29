<template>
  <div class="flex min-h-screen bg-[#faf5ee] font-sans">

    <!-- ── Sidebar ── -->
    <aside class="fixed top-0 left-0 h-full w-[150px] bg-[#f5ede3] border-r border-[#e8ddd0] flex flex-col items-center py-10 gap-6 z-40">

      <!-- Logo -->
      <NuxtLink to="/" class="flex flex-col items-center gap-1 mb-10">
        <img src="@/assets/images/logo/dashboard-logo.png" alt="Credeny" class="w-full h-20" />
      </NuxtLink>

      <!-- Nav items -->
      <nav class="flex flex-col items-center gap-10 mt-10 flex-1">
        <NuxtLink
          v-for="item in navItems"
          :key="item.label"
          :to="item.href"
          class="flex flex-col items-center gap-1 w-full py-2.5 px-1 rounded-xl transition-all duration-200 group"
          active-class="!bg-[#90D0FF]"
        >
          <div
            class="w-12 h-12 rounded-full flex items-center justify-center transition-colors duration-200 group-[.router-link-active]:bg-[#c8873a]"
            :class="item.iconBg"
          >
            <img :src="item.icon" class="w-full h-full" />
          </div>

          <span class="font-semibold text-[#1a1a2e] group-[.router-link-active]:text-white leading-none">
            {{ item.label }}
          </span>
        </NuxtLink>
      </nav>

      <!-- Sign Out -->
      <button
        @click="handleSignOut"
        class="flex flex-col items-center gap-1 w-full py-2.5 px-1 rounded-xl hover:bg-red-50 transition-colors duration-200 group"
      >
        <div class="w-9 h-9 rounded-full flex items-center justify-center bg-red-100 group-hover:bg-red-200 transition-colors duration-200">
          <svg class="w-5 h-5 text-red-500" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1"/>
          </svg>
        </div>
        <span class="text-[0.6rem] font-semibold text-red-500 leading-none">Sign Out</span>
      </button>
    </aside>

    <!-- ── Main area ── -->
    <div class="flex-1 flex flex-col ml-[200px]">

      <!-- Topbar -->
      <header class="sticky top-0 z-30 bg-[#faf5ee] border-b border-[#e8ddd0] h-[100px] flex items-center px-20 gap-4">
        <!-- Search -->
        <div class="flex items-center gap-2 bg-white border border-[#e8ddd0] rounded-lg px-3.5 py-2 w-full max-w-xs">
          <svg class="w-4 h-4 text-[#bbb] flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-4.35-4.35M17 11A6 6 0 115 11a6 6 0 0112 0z"/>
          </svg>
          <input
            v-model="searchQuery"
            type="text"
            placeholder="Search for Badge"
            class="text-sm text-[#333] placeholder-[#bbb] bg-transparent outline-none w-full"
          />
        </div>

        <!-- Spacer -->
        <div class="flex-1"></div>

        <!-- User -->
        <div class="flex items-center gap-2.5 cursor-pointer group">
          <img
            src="@/assets/images/icons/avatar.png"
            alt="User avatar"
            class="w-12 h-12 rounded-full object-cover border-2 border-[#e8ddd0] group-hover:border-[#c8873a] transition-colors duration-200"
          />
          <span class="text-sm font-semibold text-[#1a1a2e] hidden sm:block">Mathew Key</span>
        </div>
      </header>

      <!-- Page content -->
      <main class="flex-1 p-20">
        <slot />
      </main>
    </div>
  </div>
</template>

<script setup>
import { ref, h } from 'vue'
import shelfIcon from '@/assets/images/icons/shelf.png'
import accountIcon from '@/assets/images/icons/user.png'

const searchQuery = ref('')

// ── Sidebar icons ──

const navItems = [
  { label: 'Shelf',      href: '/user/dashboard/shelf',      icon: shelfIcon,      iconBg: 'bg-[#e8ddd0]' },
    { label: 'Collection',    href: '/user/dashboard/collections',    icon: accountIcon,    iconBg: 'bg-[#e8ddd0]' },
    { label: 'Account',    href: '/user/dashboard/account',    icon: accountIcon,    iconBg: 'bg-[#e8ddd0]' },
  ]

const handleSignOut = async () => {
  // Add your sign out logic here
  await navigateTo('/login')
}
</script>
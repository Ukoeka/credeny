<template>
  <div class="flex min-h-screen bg-[#faf5ee] font-sans">

    <!-- ── Sidebar ── -->
    <aside class="fixed top-0 left-0 h-full w-[150px] bg-[#f5ede3] border-r border-[#e8ddd0] flex flex-col items-center py-5 gap-6 z-40">

      <!-- Logo -->
      <NuxtLink to="/" class="flex flex-col items-center gap-1 mb-2">
        <img src="@/assets/images/logo/logo.png" alt="Credeny" class="w-full h-9" />
      </NuxtLink>

      <!-- Nav items -->
      <nav class="flex flex-col items-center gap-1 flex-1">
        <NuxtLink
          v-for="item in navItems"
          :key="item.label"
          :to="item.href"
          class="flex flex-col items-center gap-1 w-full py-2.5 px-1 rounded-xl transition-all duration-200 group"
          active-class="!bg-[#1a1a2e]"
        >
          <div
            class="w-9 h-9 rounded-full flex items-center justify-center transition-colors duration-200 group-[.router-link-active]:bg-[#c8873a]"
            :class="item.iconBg"
          >
            <component :is="item.icon" class="w-5 h-5 text-[#1a1a2e] group-[.router-link-active]:text-white" />
          </div>
          <span class="text-[0.6rem] font-semibold text-[#1a1a2e] group-[.router-link-active]:text-white leading-none">
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
      <header class="sticky top-0 z-30 bg-[#faf5ee] border-b border-[#e8ddd0] h-[56px] flex items-center px-6 gap-4">
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
            class="w-8 h-8 rounded-full object-cover border-2 border-[#e8ddd0] group-hover:border-[#c8873a] transition-colors duration-200"
          />
          <span class="text-sm font-semibold text-[#1a1a2e] hidden sm:block">Mathew Key</span>
        </div>
      </header>

      <!-- Page content -->
      <main class="flex-1 p-6">
        <slot />
      </main>
    </div>
  </div>
</template>

<script setup>
import { ref, h } from 'vue'

const searchQuery = ref('')

// ── Sidebar icons ──
const IconShelf = { render: () => h('svg', { fill: 'none', viewBox: '0 0 24 24', stroke: 'currentColor', 'stroke-width': '2' }, [h('path', { 'stroke-linecap': 'round', 'stroke-linejoin': 'round', d: 'M4 7h16M4 12h16M4 17h16' })]) }
const IconCollection = { render: () => h('svg', { fill: 'none', viewBox: '0 0 24 24', stroke: 'currentColor', 'stroke-width': '2' }, [h('path', { 'stroke-linecap': 'round', 'stroke-linejoin': 'round', d: 'M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10' })]) }
const IconAccount = { render: () => h('svg', { fill: 'none', viewBox: '0 0 24 24', stroke: 'currentColor', 'stroke-width': '2' }, [h('path', { 'stroke-linecap': 'round', 'stroke-linejoin': 'round', d: 'M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z' })]) }

const navItems = [
  { label: 'Shelf',      href: '/dashboard/shelf',      icon: IconShelf,      iconBg: 'bg-[#e8ddd0]' },
  { label: 'Collection', href: '/dashboard/collection', icon: IconCollection, iconBg: 'bg-[#e8ddd0]' },
  { label: 'Account',    href: '/dashboard/account',    icon: IconAccount,    iconBg: 'bg-[#e8ddd0]' },
]

const handleSignOut = async () => {
  // Add your sign out logic here
  await navigateTo('/login')
}
</script>
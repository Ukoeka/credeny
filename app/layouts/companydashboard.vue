<template>
  <div class="flex min-h-screen bg-[#faf5ee] font-sans">

    <!-- ── Sidebar ── -->
    <aside class="fixed top-0 left-0 h-full w-[120px] bg-[#f5ede3] border-r border-[#e8ddd0] flex flex-col items-center py-5 gap-6 z-40">

      <!-- Logo -->
      <NuxtLink to="/" class="flex flex-col items-center gap-1 mb-2">
        <img src="@/assets/images/logo/dashboard-logo.png" alt="Credeny" class="w-full" />
      </NuxtLink>

      <!-- Nav items -->
      <nav class="flex flex-col items-center gap-1 flex-1 w-full px-2">
        <NuxtLink
          v-for="item in navItems"
          :key="item.label"
          :to="item.href"
          class="flex flex-col items-center gap-1 w-full py-2.5 px-1 rounded-xl transition-all duration-200 group"
          active-class="bg-[#1a1a2e]"
        >
          <div
            class="w-9 h-9 rounded-full flex items-center justify-center transition-colors duration-200 bg-[#e8ddd0] group-[.bg-\[\#1a1a2e\]]:bg-[#c8873a]"
          >
            <component :is="item.icon" class="w-5 h-5 text-[#1a1a2e] group-[.bg-\[\#1a1a2e\]]:text-white" />
          </div>
          <span class="text-[0.6rem] font-semibold text-[#1a1a2e] group-[.bg-\[\#1a1a2e\]]:text-white leading-none text-center">
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
    <div class="flex-1 flex flex-col ml-[120px]">

      <!-- Topbar -->
      <header class="sticky top-0 z-30 bg-[#faf5ee] border-b border-[#e8ddd0] h-[100px] flex items-center px-6 gap-4">
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
        <div class="flex-1"></div>
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
const IconBadges = { render: () => h('svg', { fill: 'none', viewBox: '0 0 24 24', stroke: 'currentColor', 'stroke-width': '2' }, [h('path', { 'stroke-linecap': 'round', 'stroke-linejoin': 'round', d: 'M9 12l2 2 4-4M7.835 4.697a3.42 3.42 0 001.946-.806 3.42 3.42 0 014.438 0 3.42 3.42 0 001.946.806 3.42 3.42 0 013.138 3.138 3.42 3.42 0 00.806 1.946 3.42 3.42 0 010 4.438 3.42 3.42 0 00-.806 1.946 3.42 3.42 0 01-3.138 3.138 3.42 3.42 0 00-1.946.806 3.42 3.42 0 01-4.438 0 3.42 3.42 0 00-1.946-.806 3.42 3.42 0 01-3.138-3.138 3.42 3.42 0 00-.806-1.946 3.42 3.42 0 010-4.438 3.42 3.42 0 00.806-1.946 3.42 3.42 0 013.138-3.138z' })]) }
const IconAwardees = { render: () => h('svg', { fill: 'none', viewBox: '0 0 24 24', stroke: 'currentColor', 'stroke-width': '2' }, [h('path', { 'stroke-linecap': 'round', 'stroke-linejoin': 'round', d: 'M12 14l-3-3m0 0l3-3m-3 3h8M5 12a7 7 0 1114 0 7 7 0 01-14 0z' }), h('path', { 'stroke-linecap': 'round', 'stroke-linejoin': 'round', d: 'M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z' })]) }
const IconGroups = { render: () => h('svg', { fill: 'none', viewBox: '0 0 24 24', stroke: 'currentColor', 'stroke-width': '2' }, [h('path', { 'stroke-linecap': 'round', 'stroke-linejoin': 'round', d: 'M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z' })]) }
const IconAccount = { render: () => h('svg', { fill: 'none', viewBox: '0 0 24 24', stroke: 'currentColor', 'stroke-width': '2' }, [h('path', { 'stroke-linecap': 'round', 'stroke-linejoin': 'round', d: 'M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z' })]) }

const navItems = [
  { label: 'Badges',   href: '/issuer/dashboard/badges',   icon: IconBadges   },
  { label: 'Awardees', href: '/issuer/dashboard/awardees', icon: IconAwardees },
  { label: 'Groups',   href: '/issuer/dashboard/groups',   icon: IconGroups   },
  { label: 'Account',  href: '/issuer/dashboard/account',  icon: IconAccount  },
]

const handleSignOut = async () => {
  await navigateTo('/login')
}
</script>
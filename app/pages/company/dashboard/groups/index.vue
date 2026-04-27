<template>
  <div>

    <!-- ── Hero Banner ── -->
    <div class="relative w-full rounded-2xl overflow-hidden mb-8 h-[130px] flex items-center justify-center">
      <img src="@/assets/images/backgrounds/dashboard-banner.png" alt="" class="absolute inset-0 w-full h-full object-cover" />
      <div class="absolute inset-0 bg-black/15"></div>

      <!-- Create Group button -->
      <NuxtLink
        to="/company/dashboard/groups/create"
        class="absolute top-4 right-4 z-20 flex items-center gap-2 text-xs font-semibold text-[#1a1a2e] bg-white/90 hover:bg-white px-3 py-2 rounded-lg shadow transition-all duration-200 backdrop-blur-sm whitespace-nowrap"
      >
        Create Group
        <div class="w-5 h-5 rounded-full bg-[#1a1a2e] flex items-center justify-center flex-shrink-0">
          <svg class="w-3 h-3 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="3">
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 4v16m8-8H4"/>
          </svg>
        </div>
      </NuxtLink>

      <div class="relative z-10 text-center">
        <h1 class="text-3xl lg:text-4xl font-extrabold text-[#1a1a2e] tracking-tight">Groups</h1>
        <p class="text-[#333] text-sm mt-1">Create groups to easily manage awardees</p>
      </div>
    </div>

    <!-- ── Table card ── -->
    <div class="bg-white rounded-2xl border border-[#f0e6d8] overflow-hidden">
      <div class="overflow-x-auto">
        <table class="w-full text-sm">
          <thead>
            <tr class="border-b border-[#f0e6d8]">
              <th class="text-left px-5 py-4 text-xs font-semibold text-[#aaa] w-[110px]">Serial Number</th>
              <th class="text-left px-4 py-4 text-xs font-semibold text-[#aaa] cursor-pointer hover:text-[#1a1a2e] transition-colors duration-200" @click="sortGroups">
                <div class="flex items-center gap-1">
                  Group Name
                  <svg class="w-3 h-3" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7"/>
                  </svg>
                </div>
              </th>
              <th class="text-left px-4 py-4 text-xs font-semibold text-[#aaa]">Badges</th>
              <th class="text-left px-4 py-4 text-xs font-semibold text-[#aaa]">Awardees</th>
              <th class="text-left px-4 py-4 text-xs font-semibold text-[#aaa]">Date Created</th>
              <th class="w-8"></th>
            </tr>
          </thead>
          <tbody class="divide-y divide-[#f7f0e8]">
            <tr
              v-for="(group, i) in groups"
              :key="group.id"
              class="hover:bg-[#fdf9f5] transition-colors duration-150 group cursor-pointer"
              @click="navigateTo(`/company/dashboard/groups/${group.id}`)"
            >
              <td class="px-5 py-4 text-xs text-[#aaa]">{{ i + 1 }}</td>
              <td class="px-4 py-4 font-bold text-[#1a1a2e]">{{ group.name }}</td>
              <td class="px-4 py-4 text-[#555]">{{ group.badges }}</td>
              <td class="px-4 py-4 text-[#555]">{{ group.awardees }}</td>
              <td class="px-4 py-4 text-[#888]">{{ group.dateCreated }}</td>
              <td class="px-3 py-4">
                <button
                  class="p-1 rounded-md opacity-0 group-hover:opacity-100 hover:bg-[#f0e6d8] transition-all duration-200"
                  @click.stop="openMenu(group.id)"
                >
                  <svg class="w-4 h-4 text-[#aaa]" fill="currentColor" viewBox="0 0 24 24">
                    <path d="M12 13a1 1 0 110-2 1 1 0 010 2zm0-5a1 1 0 110-2 1 1 0 010 2zm0 10a1 1 0 110-2 1 1 0 010 2z"/>
                  </svg>
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

  </div>
</template>

<script setup>
definePageMeta({ layout: 'companydashboard' })

const openMenu = (id) => console.log('menu', id)

const sortGroups = () => {
  groups.value.sort((a, b) => a.name.localeCompare(b.name))
}

const groups = ref([
  { id: 1, name: 'LEarning Group 1', badges: 13, awardees: 22, dateCreated: '13 April 2024' },
  { id: 2, name: 'Class 1',          badges: 13, awardees: 22, dateCreated: '13 April 2024' },
  ...Array.from({ length: 13 }, (_, i) => ({
    id: i + 3,
    name: 'LEarning Group 1',
    badges: 13,
    awardees: 22,
    dateCreated: '13 April 2024',
  })),
])

useHead({ title: 'Groups — Credeny Issuer' })
</script>
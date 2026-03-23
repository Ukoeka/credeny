<template>
  <div>
    <!-- Back button -->
    <button
      @click="$router.back()"
      class="flex items-center justify-center w-8 h-8 rounded-full bg-[#1a1a2e] hover:bg-[#2d2d4e] text-white transition-colors duration-200 mb-6"
    >
      <svg class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
        <path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7"/>
      </svg>
    </button>

    <div class="bg-white rounded-2xl border border-[#f0e6d8] p-8">

      <!-- ── Header: badge image + title + actions ── -->
      <div class="flex flex-col sm:flex-row gap-6 mb-8">
        <!-- Badge image -->
        <div class="flex-shrink-0">
          <img
            :src="badge.image"
            :alt="badge.title"
            class="w-100 h-100 rounded-full object-cover border-4 border-[#f5ede3]"
          />
        </div>

        <!-- Title + meta + actions -->
        <div class="flex-1 min-w-0">
          <div class="flex flex-col sm:flex-row sm:items-start justify-between gap-4">
            <div>
              <h1 class="text-xl font-extrabold text-[#1a1a2e] tracking-tight mb-1">
                {{ badge.title }}
              </h1>
              <p class="text-sm text-[#888]">Awarded to <span class="font-medium text-[#555]">{{ badge.awardedTo }}</span></p>
              <p class="text-sm text-[#888]">Issued on <span class="font-medium text-[#555]">{{ badge.issuedDate }}</span></p>
            </div>

            <!-- Action buttons -->
            <div class="flex items-center gap-2 flex-shrink-0">
              <button class="text-xs font-semibold text-[#1a1a2e] border border-[#1a1a2e]/20 px-4 py-2 rounded-lg hover:bg-[#1a1a2e] hover:text-white transition-all duration-200">
                Manage Badge
              </button>
              <!-- Visibility toggle -->
              <button class="w-9 h-9 flex items-center justify-center rounded-lg border border-[#e8ddd0] hover:bg-[#f5ede3] transition-colors duration-200">
                <svg class="w-4 h-4 text-[#888]" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M13.875 18.825A10.05 10.05 0 0112 19c-4.478 0-8.268-2.943-9.543-7a9.97 9.97 0 011.563-3.029m5.858.908a3 3 0 114.243 4.243M9.878 9.878l4.242 4.242M9.88 9.88l-3.29-3.29m7.532 7.532l3.29 3.29M3 3l3.59 3.59m0 0A9.953 9.953 0 0112 5c4.478 0 8.268 2.943 9.543 7a10.025 10.025 0 01-4.132 5.411m0 0L21 21"/>
                </svg>
              </button>
              <!-- Download -->
              <button class="w-9 h-9 flex items-center justify-center rounded-lg border border-[#e8ddd0] hover:bg-[#f5ede3] transition-colors duration-200">
                <svg class="w-4 h-4 text-[#888]" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"/>
                </svg>
              </button>
              <!-- Share -->
              <button class="w-9 h-9 flex items-center justify-center rounded-lg border border-[#e8ddd0] hover:bg-[#f5ede3] transition-colors duration-200">
                <svg class="w-4 h-4 text-[#888]" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M8.684 13.342C8.886 12.938 9 12.482 9 12c0-.482-.114-.938-.316-1.342m0 2.684a3 3 0 110-2.684m0 2.684l6.632 3.316m-6.632-6l6.632-3.316m0 0a3 3 0 105.367-2.684 3 3 0 00-5.367 2.684zm0 9.316a3 3 0 105.368 2.684 3 3 0 00-5.368-2.684z"/>
                </svg>
              </button>
            </div>
          </div>
        </div>
      </div>

      <!-- ── Description ── -->
      <p class="text-sm text-[#555] leading-relaxed mb-8">
        {{ badge.description }}
      </p>

      <!-- ── Issuer ── -->
      <div class="flex items-center gap-3 py-4 border-t border-b border-[#f0e6d8] mb-8">
        <span class="text-sm font-semibold text-[#1a1a2e]">Issuer :</span>
        <img
          :src="badge.issuerLogo"
          alt=""
          class="w-6 h-6 rounded-full object-cover"
        />
        <span class="text-sm text-[#555]">{{ badge.issuer }}</span>
      </div>

      <!-- ── Earning Criteria ── -->
      <div class="mb-8">
        <h2 class="text-sm font-extrabold text-[#1a1a2e] uppercase tracking-wider mb-4">
          Earning Criteria
        </h2>
        <ul class="space-y-2">
          <li
            v-for="criterion in badge.criteria"
            :key="criterion"
            class="flex items-start gap-2 text-sm text-[#555]"
          >
            <span class="mt-1.5 w-1.5 h-1.5 rounded-full bg-[#555] flex-shrink-0"></span>
            {{ criterion }}
          </li>
        </ul>
      </div>

      <!-- ── Proof of Criteria Completion ── -->
      <div>
        <h2 class="text-sm font-extrabold text-[#1a1a2e] mb-3">
          Proof of Criteria Completion
        </h2>
        <p class="text-sm text-[#555] leading-relaxed">
          {{ badge.proof }}
        </p>
      </div>

    </div>
  </div>
</template>

<script setup>
definePageMeta({ layout: 'dashboard' })

const route = useRoute()

// Replace with real API call using route.params.id
const badge = ref({
  id: route.params.id,
  title: 'Badge of Excellence',
  awardedTo: 'Favoudoh (Favoudoh@gmail.com)',
  issuedDate: '4th April 2024',
  image: '/images/randoms/badge.png',
  issuer: 'Robbert Greed Foundation',
  issuerLogo: '@/assets/images/issuers/issuer-logo.png',
  description: `Lorem ipsum dolor sit amet consectetur. Magnis faucibus quis facilisis mattis sit urna felis scelerisque. Ullamcorper at interdum tortor sed sem neque. Facilisi nisl sem volutpat diam ultricies ac. Duis condimentum arcu diam non velit.

Vitae est eleifend molestie mi eget. Odio quis amet vel magna quis fringilla faucibus. Leo id tellus molestie id. Facilisis sit condimentum massa sapien. Scelerisque urna placerat in ipsum mi. Morbi non sit aliquet suspendisse enim. Diam nibh vitae ipsum tortor tellus in non enim. Velit tincidunt tortor aenean erat luctus quis dignissim id. In quis ultrices enim habitant nunc ultrices sed. Maecenas augue sed donec vulputate. Tristique urna egestas ornare id.`,
  criteria: [
    'Lorem ipsum dolor sit amet consectetur.',
    'Magnis faucibus quis facilisis mattis sit urna felis scelerisque.',
    'Ullamcorper at interdum tortor sed sem neque.',
    'Facilisi nisl sem volutpat diam ultricies ac. Duis condimentum arcu diam non velit.',
    'Vitae est eleifend molestie mi eget',
  ],
  proof: `Lorem ipsum dolor sit amet consectetur. Magnis faucibus quis facilisis mattis sit urna felis scelerisque. Ullamcorper at interdum tortor sed sem neque. Facilisi nisl sem volutpat diam ultricies ac. Duis condimentum arcu diam non velit.`,
})

useHead({ title: `${badge.value.title} — Credeny` })
</script>
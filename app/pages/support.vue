<template>
  <SharedLayout>


    <section class="relative pt-[68px] min-h-[450px] flex items-center justify-center overflow-hidden">
      <!-- Background image — add your image here -->
      <img
        src="@/assets/images/backgrounds/support-bg.png"
        alt=""
        class="absolute inset-0 w-full h-full object-cover"
      />
      <!-- Dark overlay -->
      <div class="absolute inset-0 bg-black/55"></div>

      <!-- Content -->
      <div class="relative z-10 text-center px-6 py-20 max-w-2xl mx-auto">
        <h1 class="text-3xl lg:text-4xl font-extrabold text-white mb-5 tracking-tight leading-tight">
          Welcome To The Credeny Support Center!
        </h1>
        <p class="text-white/75 text-sm lg:text-base leading-relaxed mb-10">
          At Credeny, We're Committed To Providing You With Exceptional Support To Ensure Your
          Experience With Our Platform Is Smooth And Seamless. Below, You'll Find Various Resources
          To Assist You In Navigating Our Services And Resolving Any Issues You May Encounter.
        </p>

        <!-- Search bar -->
        <div class="flex items-center max-w-md mx-auto rounded-lg overflow-hidden shadow-lg">
          <div class="flex items-center flex-1 bg-white px-4 py-3 gap-2">
            <svg class="w-4 h-4 text-[#aaa] flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-4.35-4.35M17 11A6 6 0 115 11a6 6 0 0112 0z"/>
            </svg>
            <input
              v-model="searchQuery"
              type="text"
              placeholder="Enter Keyword"
              class="flex-1 text-sm text-[#333] placeholder-[#bbb] bg-transparent outline-none"
              @keyup.enter="handleSearch"
            />
          </div>
          <button
            @click="handleSearch"
            class="bg-[#c8873a] hover:bg-[#b5762f] text-white font-semibold text-sm px-6 py-3 transition-colors duration-200 whitespace-nowrap"
          >
            Search
          </button>
        </div>
      </div>
    </section>

  
    <section class="bg-black text-white py-20 border-b border-gray-300" >
      <div class="max-w-[1200px] mx-auto px-6 lg:px-10 grid lg:grid-cols-2  gap-16 ">

        <!-- Left: description -->
        <div class="">
          <h2 class="text-[30px] font-extrabold mb-5 tracking-tight">FAQs</h2>
          <p class="text-white/60 mb-8">
            Our FAQs section covers a wide range of common queries and concerns. Before reaching out to our
            support team, we recommend checking here for quick answers to your questions.
          </p>
          <NuxtLink
            to="/#contact"
            class="inline-block text-sm font-semibold text-white border border-white/40 px-3 py-2.5 rounded-lg hover:bg-white hover:text-[#1a1a2e] transition-all duration-200"
          >
            Contact
          </NuxtLink>
        </div>

        <!-- Right: accordion -->
        <div class="divide-y divide-white/10">
          <div
            v-for="(faq, i) in faqs"
            :key="i"
            class="py-5 border-b border-gray-300 py-10"
          >
            <button
              class="w-full flex items-center justify-between gap-4 text-left group"
              @click="toggleFaq(i)"
            >
              <span
                class="text-sm font-semibold text-white/90 group-hover:text-white transition-colors duration-200"
                :class="openFaq === i ? 'text-white' : ''"
              >
                {{ faq.question }}
              </span>
              <svg
                class="w-5 h-5 flex-shrink-0 text-white/50 transition-transform duration-300"
                :class="openFaq === i ? 'rotate-180 text-[#c8873a]' : ''"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
                stroke-width="2"
              >
                <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7"/>
              </svg>
            </button>

            <!-- Answer -->
            <div
              class="overflow-hidden transition-all duration-300 ease-in-out"
              :class="openFaq === i ? 'max-h-96 mt-4' : 'max-h-0'"
            >
              <p class="text-white/60 text-sm leading-relaxed">
                {{ faq.answer }}
              </p>
            </div>
          </div>
        </div>

      </div>
      
    </section>

  </SharedLayout>
</template>

<script setup>
import { ref } from 'vue'

const searchQuery = ref('')
const openFaq = ref(null)

const handleSearch = () => {
  // Handle search logic
  console.log('Searching for:', searchQuery.value)
}

const toggleFaq = (index) => {
  openFaq.value = openFaq.value === index ? null : index
}

const faqs = [
  {
    question: 'Question Lorem Ipsum',
    answer: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris.',
  },
  {
    question: 'Question Lorem Ipsum',
    answer: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris.',
  },
  {
    question: 'Question Lorem Ipsum',
    answer: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris.',
  },
  {
    question: 'Question Lorem Ipsum',
    answer: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris.',
  },
  {
    question: 'Question Lorem Ipsum',
    answer: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris.',
  },
]

useHead({
  title: 'Support Center — Credeny',
  meta: [
    { name: 'description', content: 'Get help and find answers to common questions about Credeny\'s digital credentialing platform.' },
  ],
})
</script>
<template>
  <div class="font-sans bg-[#f5ede3] overflow-x-hidden">
    <AppHeader />
    
    <main>
      <slot />
    </main>
    
    <AppFooter />
  </div>
</template>

<script setup>
import AppHeader from './Header.vue'
import AppFooter from './Footer.vue'
</script>

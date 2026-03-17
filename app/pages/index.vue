<template>
  <SharedLayout>
    <!-- ═══════════════════════════════════════════
         HERO SECTION
    ═══════════════════════════════════════════ -->
      <section
        id="home"
        class="relative min-h-screen bg-[#f5ede3] flex items-center pt-[68px] overflow-hidden"
      >
        <!-- Subtle background pattern -->
        <div class="absolute inset-0 pointer-events-none opacity-[0.04]"
          style="background-image: radial-gradient(circle, #1a1a2e 1px, transparent 1px); background-size: 30px 30px;">
        </div>

        <div class="max-w-[1200px] mx-auto px-6 lg:px-10 w-full grid lg:grid-cols-2 gap-12 items-center py-20">
          <!-- Left: copy -->
          <div class="hero-text">
            <h1 class="text-[clamp(2.4rem,5vw,3.8rem)] font-extrabold leading-[1.1] tracking-tight text-[#1a1a2e] mb-6">
              Showcase Your<br />
              Achievements And<br />
              <span class="text-[#c8873a]">Digital Credentials</span>
            </h1>
            <p class="text-[#555] text-base lg:text-lg leading-relaxed mb-10 max-w-sm">
              Secure, verifiable, and easily shareable digital certificates and Badges
            </p>
            <NuxtLink
              to="/signup"
              class="inline-block bg-[#1a1a2e] text-white font-bold text-sm px-7 py-3.5 rounded-lg hover:bg-[#2d2d4e] transition-all duration-200 hover:-translate-y-0.5 shadow-md hover:shadow-lg"
            >
              Get Started
            </NuxtLink>

            <!-- Trust badges -->
            <div class="flex items-center gap-6 mt-12">
              <div class="flex flex-col">
                <span class="text-2xl font-extrabold text-[#1a1a2e]">50K+</span>
                <span class="text-xs text-[#888] font-medium">Credentials Issued</span>
              </div>
              <div class="w-px h-10 bg-[#ddd]"></div>
              <div class="flex flex-col">
                <span class="text-2xl font-extrabold text-[#1a1a2e]">1.2K+</span>
                <span class="text-xs text-[#888] font-medium">Organizations</span>
              </div>
              <div class="w-px h-10 bg-[#ddd]"></div>
              <div class="flex flex-col">
                <span class="text-2xl font-extrabold text-[#1a1a2e]">99%</span>
                <span class="text-xs text-[#888] font-medium">Satisfaction Rate</span>
              </div>
            </div>
          </div>

          <!-- Right: hero image placeholder -->
          <div class="relative flex justify-center lg:justify-end hero-image-wrap">
            <!-- Blob background shape -->
            <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[420px] h-[420px] rounded-[60%_40%_55%_45%/50%_60%_40%_50%] bg-[#e8d5be] opacity-70 -z-0"></div>
            <img src="@/assets/images/landing/hero.png" alt="">
          

            <!-- Floating card decoration -->
            <div class="absolute -bottom-4 -left-4 lg:left-4 bg-white rounded-xl shadow-xl px-4 py-3 flex items-center gap-3 z-20">
             
              <div>
                <p class="text-xs font-bold text-[#1a1a2e]">Verified Badge</p>
                <p class="text-[10px] text-[#888]">Instantly shareable</p>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ═══════════════════════════════════════════
           WHAT ARE DIGITAL CREDENTIALS
      ═══════════════════════════════════════════ -->
      <section
        id="features"
        class="relative bg-[#1a1a2e] text-white py-24 overflow-hidden"
      >
        <!-- Topographic pattern overlay -->
        <div class="absolute inset-0 opacity-[0.06] pointer-events-none"
          style="background-image: repeating-linear-gradient(0deg, transparent, transparent 40px, rgba(255,255,255,0.3) 40px, rgba(255,255,255,0.3) 41px), repeating-linear-gradient(90deg, transparent, transparent 40px, rgba(255,255,255,0.3) 40px, rgba(255,255,255,0.3) 41px);">
        </div>

        <div class="max-w-[1200px] mx-auto px-6 lg:px-10 text-center relative z-10">
          <h2 class="text-3xl lg:text-4xl font-extrabold mb-5 tracking-tight">
            What Are Digital Credentials?
          </h2>
          <p class="text-[#ccc] text-sm lg:text-base leading-relaxed max-w-2xl mx-auto">
            Digital Credentials Are The Modern Way To Display Your Skills And Achievements.
            They Are Secure, Verifiable, And Easily Shareable Across Multiple Platforms. Whether You're An Educational Institution,
            A Certification Body, Or A Professional, Digital Credentials Help You Stand Out.
          </p>

          <!-- Feature cards -->
          <div class="grid sm:grid-cols-3 gap-5 mt-16">
            <div
              v-for="card in featureCards"
              :key="card.title"
              class="bg-white/5 border border-white/10 rounded-2xl p-7 text-left hover:bg-white/10 hover:border-[#c8873a]/40 transition-all duration-300 group"
            >
              <div class="w-11 h-11 rounded-xl bg-[#c8873a]/15 flex items-center justify-center mb-5 group-hover:bg-[#c8873a]/25 transition-colors duration-300">
                <component :is="card.icon" class="w-5 h-5 text-[#c8873a]" />
              </div>
              <h3 class="font-bold text-base mb-2">{{ card.title }}</h3>
              <p class="text-[#aaa] text-sm leading-relaxed">{{ card.desc }}</p>
            </div>
          </div>
        </div>
      </section>

      <!-- ═══════════════════════════════════════════
           WHAT WE OFFER
      ═══════════════════════════════════════════ -->
      <section class="bg-[#faf5ee] py-24">
        <div class="max-w-[1200px] mx-auto px-6 lg:px-10 grid lg:grid-cols-2 gap-16 items-center">

          <!-- Left: text -->
          <div>
            <p class="text-[#c8873a] font-bold text-sm uppercase tracking-widest mb-3">Platform</p>
            <h2 class="text-3xl lg:text-4xl font-extrabold text-[#1a1a2e] mb-5 tracking-tight leading-tight">
              What We Offer
            </h2>
            <p class="text-[#666] text-sm lg:text-base leading-relaxed mb-10">
              Credeny is a digital credentialing platform that enables organizations to issue, manage,
              and verify credentials in a secure and transparent way. Our platform provides a solution for:
            </p>

            <div class="space-y-7">
              <div
                v-for="offer in offers"
                :key="offer.title"
                class="flex gap-4 group"
              >
                <div class="flex-shrink-0 mt-0.5">
                  <div class="w-9 h-9 rounded-full border-2 border-[#c8873a] flex items-center justify-center group-hover:bg-[#c8873a] transition-colors duration-200">
                    <svg class="w-4 h-4 text-[#c8873a] group-hover:text-white transition-colors duration-200" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                      <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7"/>
                    </svg>
                  </div>
                </div>
                <div>
                  <h3 class="font-bold text-[#c8873a] text-base mb-1">{{ offer.title }}</h3>
                  <p class="text-[#666] text-sm leading-relaxed">{{ offer.desc }}</p>
                </div>
              </div>
            </div>
          </div>

          <!-- Right: app mockup placeholder -->
          <div class="relative">
            <!-- Browser chrome mockup -->
            <div class="bg-white rounded-2xl shadow-2xl overflow-hidden border border-[#eee]">
              <!-- Browser bar -->
              <div class="bg-[#f0f0f0] px-4 py-3 flex items-center gap-2 border-b border-[#e0e0e0]">
                <div class="flex gap-1.5">
                  <div class="w-3 h-3 rounded-full bg-[#ff5f57]"></div>
                  <div class="w-3 h-3 rounded-full bg-[#febc2e]"></div>
                  <div class="w-3 h-3 rounded-full bg-[#28c840]"></div>
                </div>
                <div class="flex-1 bg-white rounded-md h-6 mx-4 flex items-center px-3">
                  <svg class="w-3 h-3 text-[#bbb] mr-1.5 flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"/></svg>
                  <span class="text-[10px] text-[#aaa]">credeny.io</span>
                </div>
              </div>
              <!-- App content area — swap with <img src="..." class="w-full" /> -->
              <div class="flex">
                <!-- Sidebar -->
                <div class="w-16 bg-[#1a1a2e] flex flex-col items-center py-4 gap-5 flex-shrink-0">
                  <div class="w-8 h-8 rounded-lg bg-[#c8873a]/20 flex items-center justify-center">
                    <div class="w-4 h-4 rounded-full border-2 border-[#c8873a]"></div>
                  </div>
                  <div v-for="i in 4" :key="i" class="w-8 h-8 rounded-lg bg-white/5 flex items-center justify-center">
                    <div class="w-4 h-1 bg-white/20 rounded"></div>
                  </div>
                </div>
                <!-- Main content mockup -->
                <div class="flex-1 p-5 bg-[#f8f8f8]">
                  <div class="bg-[#1a9be8] rounded-xl h-16 mb-4 flex items-center px-4">
                    <div>
                      <p class="text-white font-bold text-sm">Badge Collection</p>
                      <p class="text-white/70 text-[10px]">Organize your badges for easy access</p>
                    </div>
                  </div>
                  <div class="grid grid-cols-2 gap-3">
                    <div v-for="col in badgeCollections" :key="col.name" class="bg-white rounded-xl p-3 shadow-sm">
                      <div class="flex gap-1 flex-wrap mb-2">
                        <div v-for="j in 4" :key="j" class="w-7 h-7 rounded-full" :class="col.colors[j-1]"></div>
                      </div>
                      <p class="text-[#1a1a2e] text-xs font-semibold">{{ col.name }}</p>
                      <p class="text-[#aaa] text-[10px]">{{ col.count }} badges</p>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ═══════════════════════════════════════════
           TESTIMONIALS
      ═══════════════════════════════════════════ -->
      <section id="testimonials" class="bg-[#f5ede3] py-24 relative overflow-hidden">
        <!-- Giant quote mark decorations -->
        <div class="absolute top-8 left-6 text-[#c8873a]/10 text-[180px] font-serif leading-none select-none pointer-events-none">"</div>
        <div class="absolute bottom-8 right-6 text-[#c8873a]/10 text-[180px] font-serif leading-none select-none pointer-events-none rotate-180">"</div>

        <div class="max-w-[1200px] mx-auto px-6 lg:px-10 relative z-10">
          <div class="text-center mb-14">
            <p class="text-[#c8873a] font-bold text-sm uppercase tracking-widest mb-3">Social Proof</p>
            <h2 class="text-3xl lg:text-4xl font-extrabold text-[#1a1a2e] tracking-tight">
              What People Say About Us
            </h2>
          </div>

          <div class="grid md:grid-cols-3 gap-6">
            <div
              v-for="(t, i) in testimonials"
              :key="t.name"
              class="bg-white rounded-2xl p-7 shadow-sm hover:shadow-md transition-shadow duration-300 flex flex-col justify-between border border-[#f0e6d8]"
              :class="i === 1 ? 'md:-translate-y-3' : ''"
            >
              <!-- Stars -->
              <div class="flex gap-1 mb-5">
                <svg v-for="s in 5" :key="s" class="w-4 h-4 text-[#c8873a]" fill="currentColor" viewBox="0 0 20 20">
                  <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"/>
                </svg>
              </div>
              <p class="text-[#444] text-sm leading-relaxed flex-1">"{{ t.quote }}"</p>
              <div class="mt-6 flex items-center gap-3">
                <div class="w-9 h-9 rounded-full bg-[#1a1a2e] flex items-center justify-center text-white text-xs font-bold flex-shrink-0">
                  {{ t.name.split(' ').map(n => n[0]).join('') }}
                </div>
                <div>
                  <p class="font-bold text-[#1a1a2e] text-sm">{{ t.name }}</p>
                  <p class="text-[#aaa] text-xs">{{ t.role }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ═══════════════════════════════════════════
           PRICING
      ═══════════════════════════════════════════ -->
      <section id="pricing" class="bg-[#1a1a2e] text-white py-24">
        <div class="max-w-[1200px] mx-auto px-6 lg:px-10">
          <div class="text-center mb-14">
            <p class="text-[#c8873a] font-bold text-sm uppercase tracking-widest mb-3">Plans</p>
            <h2 class="text-3xl lg:text-4xl font-extrabold tracking-tight">Pricing</h2>
          </div>

          <div class="grid md:grid-cols-3 gap-6 items-stretch">
            <div
              v-for="plan in plans"
              :key="plan.name"
              class="rounded-2xl p-8 flex flex-col border transition-all duration-300 hover:-translate-y-1 hover:shadow-2xl"
              :class="plan.highlight
                ? 'bg-white text-[#1a1a2e] border-[#c8873a] shadow-[0_0_40px_rgba(200,135,58,0.25)] scale-[1.03]'
                : 'bg-white/5 border-white/10 hover:border-white/25'"
            >
              <div class="mb-6">
                <p class="font-bold text-base mb-2" :class="plan.highlight ? 'text-[#1a1a2e]' : 'text-white'">
                  {{ plan.name }}
                </p>
                <p class="text-3xl font-extrabold tracking-tight" :class="plan.highlight ? 'text-[#c8873a]' : 'text-[#c8873a]'">
                  {{ plan.price }}
                </p>
                <p v-if="plan.period" class="text-xs mt-0.5" :class="plan.highlight ? 'text-[#888]' : 'text-white/40'">
                  {{ plan.period }}
                </p>
              </div>

              <ul class="space-y-3 flex-1 mb-8">
                <li v-for="feat in plan.features" :key="feat" class="flex items-start gap-2.5 text-sm" :class="plan.highlight ? 'text-[#444]' : 'text-white/70'">
                  <svg class="w-4 h-4 mt-0.5 flex-shrink-0 text-[#c8873a]" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7"/>
                  </svg>
                  {{ feat }}
                </li>
              </ul>

              <NuxtLink
                :to="plan.href"
                class="block text-center font-bold text-sm py-3 rounded-xl transition-all duration-200"
                :class="plan.highlight
                  ? 'bg-[#1a1a2e] text-white hover:bg-[#2d2d4e]'
                  : 'bg-white/10 text-white hover:bg-white/20 border border-white/20'"
              >
                Get started
              </NuxtLink>
            </div>
          </div>
        </div>
      </section>
  </SharedLayout>
</template>

<script setup>
import { h } from 'vue'

// ── Inline icon components (no external dep) ──
const IconBadge = {
  render: () => h('svg', { fill: 'none', viewBox: '0 0 24 24', stroke: 'currentColor', 'stroke-width': '2' }, [
    h('path', { 'stroke-linecap': 'round', 'stroke-linejoin': 'round', d: 'M9 12l2 2 4-4M7.835 4.697a3.42 3.42 0 001.946-.806 3.42 3.42 0 014.438 0 3.42 3.42 0 001.946.806 3.42 3.42 0 013.138 3.138 3.42 3.42 0 00.806 1.946 3.42 3.42 0 010 4.438 3.42 3.42 0 00-.806 1.946 3.42 3.42 0 01-3.138 3.138 3.42 3.42 0 00-1.946.806 3.42 3.42 0 01-4.438 0 3.42 3.42 0 00-1.946-.806 3.42 3.42 0 01-3.138-3.138 3.42 3.42 0 00-.806-1.946 3.42 3.42 0 010-4.438 3.42 3.42 0 00.806-1.946 3.42 3.42 0 013.138-3.138z' })
  ])
}
const IconShield = {
  render: () => h('svg', { fill: 'none', viewBox: '0 0 24 24', stroke: 'currentColor', 'stroke-width': '2' }, [
    h('path', { 'stroke-linecap': 'round', 'stroke-linejoin': 'round', d: 'M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z' })
  ])
}
const IconShare = {
  render: () => h('svg', { fill: 'none', viewBox: '0 0 24 24', stroke: 'currentColor', 'stroke-width': '2' }, [
    h('path', { 'stroke-linecap': 'round', 'stroke-linejoin': 'round', d: 'M8.684 13.342C8.886 12.938 9 12.482 9 12c0-.482-.114-.938-.316-1.342m0 2.684a3 3 0 110-2.684m0 2.684l6.632 3.316m-6.632-6l6.632-3.316m0 0a3 3 0 105.367-2.684 3 3 0 00-5.367 2.684zm0 9.316a3 3 0 105.368 2.684 3 3 0 00-5.368-2.684z' })
  ])
}

// ── Data ──
const featureCards = [
  {
    title: 'Secure & Tamper-Proof',
    desc: 'Every credential is cryptographically signed and stored immutably — impossible to forge or alter.',
    icon: IconShield,
  },
  {
    title: 'Instant Verification',
    desc: 'Employers and institutions can verify credentials in real-time with a single click, no manual checks needed.',
    icon: IconBadge,
  },
  {
    title: 'Easy Sharing',
    desc: 'Share your badges and certificates across LinkedIn, email, personal portfolios, and more with one link.',
    icon: IconShare,
  },
]

const offers = [
  {
    title: 'Credential Issuance',
    desc: 'Easily create and issue digital badges and certificates to recognize skills, achievements, and competencies.',
  },
  {
    title: 'Credential Management',
    desc: 'Manage and track credentials in a centralized hub, making it easy to verify and share them.',
  },
  {
    title: 'Credential Verification',
    desc: 'Allow employers and organizations to verify credentials in real-time, ensuring authenticity and trust.',
  },
]

const badgeCollections = [
  { name: 'Work Badges', count: 16, colors: ['bg-orange-400', 'bg-red-400', 'bg-blue-400', 'bg-green-400'] },
  { name: 'School Badges', count: 8, colors: ['bg-purple-400', 'bg-yellow-400', 'bg-pink-400', 'bg-teal-400'] },
  { name: 'Achievements', count: 16, colors: ['bg-indigo-400', 'bg-amber-400', 'bg-rose-400', 'bg-cyan-400'] },
  { name: "Favours", count: 16, colors: ['bg-lime-400', 'bg-fuchsia-400', 'bg-sky-400', 'bg-emerald-400'] },
]

const testimonials = [
  {
    name: 'Mathew Renny',
    role: 'HR Manager, TechCorp',
    quote: 'Switching To Digital Credentials Has Streamlined Our Certification Process And Added A Layer Of Trust And Professionalism.',
  },
  {
    name: 'Peter Metro',
    role: 'Software Engineer',
    quote: 'Credeny Has Made It Easy For Me To Share My Achievements And Medals With My Friends, Since I Have Them All In One Place.',
  },
  {
    name: 'Aloy Mutuku',
    role: 'Learning & Dev Lead',
    quote: 'Our Employees Love The Ease Of Sharing Their Accomplishments On LinkedIn And Other Platforms.',
  },
]

const plans = [
  {
    name: 'Basic',
    price: 'Free',
    period: null,
    href: '/signup',
    highlight: false,
    features: ['Basic Features', 'Up To 100 Credentials/Month', 'Email Support', 'Badge Builder'],
  },
  {
    name: 'Pro',
    price: '$49',
    period: '/Month',
    href: '/signup?plan=pro',
    highlight: true,
    features: ['Advanced Features', 'Up To 500 Credentials/Month', 'Premium Support', 'Custom Branding', 'Analytics Dashboard'],
  },
  {
    name: 'Enterprise',
    price: 'Contact Sales',
    period: null,
    href: '/contact',
    highlight: false,
    features: ['Unlimited Credentials', 'Custom Integrations', 'Dedicated Account Manager', 'SLA Guarantee', 'SSO & Advanced Security'],
  },
]

// SEO
useHead({
  title: 'Credeny — Showcase Your Digital Credentials',
  meta: [
    { name: 'description', content: 'Secure, verifiable, and easily shareable digital certificates and badges. Issue, manage, and verify credentials with Credeny.' },
  ],
  link: [
    { rel: 'preconnect', href: 'https://fonts.googleapis.com' },
    { rel: 'preconnect', href: 'https://fonts.gstatic.com', crossorigin: '' },
    { rel: 'stylesheet', href: 'https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700;800&display=swap' },
  ],
})
</script>

<style>
/* Global font applies since this is the page root */
body {
  font-family: 'DM Sans', 'Segoe UI', sans-serif;
  -webkit-font-smoothing: antialiased;
}

/* Staggered hero entrance */
.hero-text > * {
  opacity: 0;
  transform: translateY(20px);
  animation: fadeUp 0.6s ease forwards;
}
.hero-text > *:nth-child(1) { animation-delay: 0.1s; }
.hero-text > *:nth-child(2) { animation-delay: 0.22s; }
.hero-text > *:nth-child(3) { animation-delay: 0.34s; }
.hero-text > *:nth-child(4) { animation-delay: 0.46s; }

.hero-image-wrap {
  opacity: 0;
  transform: translateX(30px);
  animation: slideIn 0.7s ease 0.3s forwards;
}

@keyframes fadeUp {
  to { opacity: 1; transform: translateY(0); }
}
@keyframes slideIn {
  to { opacity: 1; transform: translateX(0); }
}
</style>
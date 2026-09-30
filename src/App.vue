<template>
  <div :class="{ dark }" class="min-h-screen bg-slate-50 text-slate-900 transition-colors duration-500 dark:bg-slate-950 dark:text-slate-100">
    <header class="fixed inset-x-0 top-0 z-50 border-b border-slate-200/80 bg-white/90 backdrop-blur-xl dark:border-white/10 dark:bg-slate-950/90">
      <nav class="mx-auto flex max-w-7xl items-center justify-between px-5 py-4">
        <a href="#home" class="font-display text-xl font-bold">TSILAVINA<span class="text-red-500">.</span></a>
        <div class="hidden gap-5 lg:flex">
          <a v-for="n in nav" :key="n[0]" :href="n[1]" @click="activeSection=n[1].slice(1)" :class="['nav-link relative py-2 text-sm font-semibold transition hover:text-red-500', activeSection === n[1].slice(1) ? 'text-red-500' : 'text-slate-700 dark:text-slate-200']"><span>{{ t(n[0]) }}</span><span v-if="activeSection === n[1].slice(1)" class="nav-active-line"></span></a>
        </div>
        <div class="flex items-center gap-2">
          <select v-model="lang" class="rounded-xl border border-slate-300 bg-white px-2 py-2 text-xs text-slate-900 dark:border-slate-700 dark:bg-slate-900 dark:text-slate-100">
            <option value="fr">FR</option><option value="en">EN</option><option value="zh">中文</option>
          </select>
          <button @click="toggleDark" class="rounded-xl border border-slate-300 px-3 py-2 text-slate-900 dark:border-slate-700 dark:text-slate-100">{{ dark ? '☀' : '☾' }}</button>
          <button @click="menu=!menu" class="rounded-xl border border-slate-300 px-3 py-2 dark:border-slate-700 lg:hidden">☰</button>
        </div>
      </nav>
      <div v-if="menu" class="border-t border-slate-200 bg-white p-4 dark:border-white/10 dark:bg-slate-950 lg:hidden">
        <a v-for="n in nav" :key="n[0]" :href="n[1]" @click="activeSection=n[1].slice(1); menu=false" :class="['relative block rounded-xl p-3 text-slate-700 hover:bg-slate-100 dark:text-slate-200 dark:hover:bg-white/5', activeSection === n[1].slice(1) ? 'bg-red-500/5 text-red-500 dark:bg-red-500/10 dark:text-red-300' : '']">{{ t(n[0]) }}<span v-if="activeSection === n[1].slice(1)" class="nav-active-line-mobile"></span></a>
      </div>
    </header>

    <main id="home">
      <section class="grid-glow min-h-screen pt-28">
        <div class="mx-auto grid max-w-7xl gap-12 px-5 py-20 lg:grid-cols-2 lg:items-center">
          <div>
            <span class="reveal inline-block rounded-full border border-red-300 bg-red-50 px-4 py-2 text-sm font-semibold text-red-600 dark:bg-red-500/10 dark:text-red-300">● {{ t('available') }}</span>
            <p class="reveal mt-6 text-sm font-bold uppercase tracking-[.25em] text-slate-500 dark:text-slate-300">Mobile & Web • Design • Cybersecurity</p>
            <h1 class="reveal mt-4 text-5xl font-bold leading-none sm:text-7xl">{{ t('hero') }} <span class="text-red-500">{{ t('accent') }}</span></h1>
            <p class="reveal mt-7 max-w-2xl text-lg leading-8 text-slate-600 dark:text-slate-400">{{ t('intro') }}</p>
            <div class="reveal mt-9 flex flex-col gap-3 sm:flex-row">
              <a href="#projects" class="rounded-full bg-red-500 px-7 py-3.5 text-center font-bold text-white">{{ t('see') }}</a>
              <a href="#contact" class="rounded-full border border-slate-300 px-7 py-3.5 text-center font-bold text-slate-900 dark:border-slate-700 dark:text-slate-100">{{ t('contact') }}</a>
            </div>
          </div>
          <div class="reveal mx-auto w-full max-w-md rounded-[2rem] border border-slate-200 bg-white p-3 shadow-2xl dark:border-white/10 dark:bg-white/[.03]">
            <img :src="photo" @error="photo='/profile-placeholder.svg'" alt="Tsilavina" class="aspect-[4/5] w-full rounded-[1.5rem] object-cover">
          </div>
        </div>
      </section>

      <section id="about" class="border-t py-24 dark:border-white/5">
        <div class="mx-auto max-w-7xl px-5">
          <p class="text-sm font-bold uppercase tracking-[.25em] text-red-500">{{ t('about') }}</p>
          <h2 class="reveal mt-3 text-4xl font-bold">{{ t('aboutTitle') }}</h2>
          <p class="reveal mt-5 max-w-3xl leading-8 text-slate-600 dark:text-slate-400">{{ t('aboutText') }}</p>
        </div>
      </section>

      <section id="formation" class="border-t bg-slate-100 py-24 dark:border-white/5 dark:bg-slate-900/40">
        <div class="mx-auto max-w-7xl px-5">
          <p class="text-sm font-bold uppercase tracking-[.25em] text-red-500">{{ t('formation') }}</p>
          <h2 class="reveal mt-3 text-4xl font-bold">{{ t('formationTitle') }}</h2>
          <div class="mt-10 grid gap-6 md:grid-cols-2">
            <article v-for="item in education" :key="item.year" class="reveal rounded-3xl border border-slate-200 bg-white p-7 shadow-sm dark:border-white/10 dark:bg-slate-950">
              <span class="inline-flex rounded-full bg-red-500/10 px-4 py-2 text-sm font-bold text-red-600 dark:text-red-300">{{ item.year }}</span>
              <h3 class="mt-5 text-2xl font-bold">{{ item.title }}</h3>
              <p class="mt-3 leading-7 text-slate-600 dark:text-slate-300">{{ item.place }}</p>
              <p v-if="item.note" class="mt-2 font-semibold text-red-500">{{ item.note }}</p>
            </article>
          </div>
        </div>
      </section>

      <section id="experience" class="border-t py-24 dark:border-white/5">
        <div class="mx-auto max-w-7xl px-5">
          <p class="text-sm font-bold uppercase tracking-[.25em] text-red-500">{{ t('experience') }}</p>
          <h2 class="reveal mt-3 text-4xl font-bold">{{ t('experienceTitle') }}</h2>
          <article class="reveal mt-10 rounded-3xl border border-slate-200 bg-white p-8 shadow-sm dark:border-white/10 dark:bg-slate-900/50">
            <div class="flex flex-col gap-3 sm:flex-row sm:items-center sm:justify-between">
              <h3 class="text-2xl font-bold">{{ t('experienceRole') }}</h3>
              <span class="rounded-full bg-red-500/10 px-4 py-2 text-sm font-semibold text-red-600 dark:text-red-300">{{ t('experienceType') }}</span>
            </div>
            <p class="mt-4 text-lg font-semibold">Madagasikara Chine Education</p>
            <p class="mt-4 max-w-3xl leading-8 text-slate-600 dark:text-slate-300">{{ t('experienceText') }}</p>
          </article>
        </div>
      </section>      

      <section id="competences" class="border-t py-24 dark:border-white/5">
        <div class="mx-auto max-w-7xl px-5">
          <p class="text-sm font-bold uppercase tracking-[.25em] text-red-500">{{ t('competences') }}</p>
          <h2 class="reveal mt-3 text-4xl font-bold">{{ t('competencesTitle') }}</h2>
          <div class="mt-10 grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
            <div v-for="group in technicalSkills" :key="group.title" class="reveal rounded-3xl border border-slate-200 bg-white p-7 dark:border-white/10 dark:bg-slate-900/50">
              <h3 class="text-xl font-bold">{{ group.title }}</h3>
              <ul class="mt-5 space-y-3">
                <li v-for="skill in group.items" :key="skill" class="flex items-center gap-2 text-slate-600 dark:text-slate-300"><span class="text-red-500">●</span>{{ skill }}</li>
              </ul>
            </div>
          </div>
        </div>
      </section>

      <section id="projects" class="border-t bg-slate-100 py-24 dark:border-white/5 dark:bg-slate-900/40">
        <div class="mx-auto max-w-7xl px-5">
          <p class="text-sm font-bold uppercase tracking-[.25em] text-red-500">{{ t('projects') }}</p>
          <h2 class="reveal mt-3 text-4xl font-bold">{{ t('projectTitle') }}</h2>
          <div class="mt-10 grid gap-6 md:grid-cols-2">
            <article v-for="p in projects" :key="p.title" class="reveal overflow-hidden rounded-3xl border border-slate-200 bg-white dark:border-white/10 dark:bg-slate-950">
              <div :class="p.g" class="aspect-video p-7"><span class="rounded-full bg-black/20 px-3 py-2 text-xs font-bold text-white">{{ p.type }}</span><p class="mt-20 text-3xl font-bold text-white">{{ p.visual }}</p></div>
              <div class="p-7"><h3 class="text-2xl font-bold">{{ p.title }}</h3><p class="mt-3 text-slate-600 dark:text-slate-300">{{ p.text }}</p></div>
            </article>
          </div>
        </div>
      </section>

      <section id="contact" class="border-t py-24 dark:border-white/5">
        <div class="mx-auto grid max-w-7xl gap-12 px-5 lg:grid-cols-2">
          <div>
            <p class="text-sm font-bold uppercase tracking-[.25em] text-red-500">{{ t('contact') }}</p>
            <h2 class="mt-3 text-4xl font-bold">{{ t('contactTitle') }}</h2>
            <p class="mt-5 text-slate-600 dark:text-slate-300">{{ t('contactText') }}</p>
            <div class="mt-8 rounded-2xl border border-slate-200 p-4 font-semibold text-slate-800 dark:border-slate-700 dark:text-slate-100">
              📍 Antananarivo, Madagascar
            </div>
            <a :href="'tel:'+cleanPhone" class="mt-3 block rounded-2xl border border-slate-200 p-4 font-semibold text-slate-800 dark:border-slate-700 dark:text-slate-100">📞 +261 34 97 534 70</a>
            <a :href="wa" target="_blank" class="mt-3 block rounded-2xl border border-slate-200 p-4 font-semibold text-slate-800 dark:border-slate-700 dark:text-slate-100">💬 WhatsApp</a>
            <div class="mt-6 grid grid-cols-2 gap-3 sm:grid-cols-3 lg:grid-cols-5">
              <a v-for="s in socials" :key="s.name" :href="s.url" target="_blank" rel="noopener noreferrer" class="social social-card group rounded-2xl border border-slate-200 bg-white p-3 text-center text-slate-700 shadow-sm dark:border-white/10 dark:bg-slate-900/70 dark:text-slate-200">
                <span class="social-icon mx-auto" :class="'social-'+s.key" aria-hidden="true">
                  <svg v-if="s.key === 'facebook'" viewBox="0 0 24 24" fill="currentColor"><path d="M14 8h3V4h-3c-3.31 0-5 1.94-5 5v3H6v4h3v8h4v-8h3.2l.8-4H13V9c0-.66.34-1 1-1Z"/></svg>
                  <svg v-else-if="s.key === 'linkedin'" viewBox="0 0 24 24" fill="currentColor"><path d="M5.2 3.5A2.2 2.2 0 1 1 5.2 7.9a2.2 2.2 0 0 1 0-4.4ZM3.3 9.2h3.8V21H3.3V9.2Zm6.2 0h3.6v1.6h.1c.5-.9 1.7-1.9 3.6-1.9 3.8 0 4.5 2.5 4.5 5.8V21h-3.8v-5.6c0-1.3 0-3-1.9-3s-2.2 1.4-2.2 2.9V21H9.5V9.2Z"/></svg>
                  <svg v-else-if="s.key === 'github'" viewBox="0 0 24 24" fill="currentColor"><path d="M12 2.2a9.8 9.8 0 0 0-3.1 19.1c.5.1.7-.2.7-.5v-1.9c-2.8.6-3.4-1.2-3.4-1.2-.5-1.2-1.1-1.5-1.1-1.5-.9-.6.1-.6.1-.6 1 .1 1.6 1 1.6 1 .9 1.6 2.4 1.1 3 .8.1-.7.4-1.1.7-1.3-2.2-.3-4.5-1.1-4.5-4.8 0-1.1.4-2 1-2.7-.1-.3-.4-1.3.1-2.7 0 0 .8-.3 2.8 1a9.6 9.6 0 0 1 5.1 0c2-1.3 2.8-1 2.8-1 .5 1.4.2 2.4.1 2.7.6.7 1 1.6 1 2.7 0 3.7-2.3 4.5-4.5 4.8.4.3.7 1 .7 1.9v2.8c0 .3.2.6.7.5A9.8 9.8 0 0 0 12 2.2Z"/></svg>
                  <svg v-else-if="s.key === 'instagram'" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><rect x="3" y="3" width="18" height="18" rx="5"/><circle cx="12" cy="12" r="4.2"/><circle cx="17.3" cy="6.8" r="1" fill="currentColor" stroke="none"/></svg>
                  <svg v-else viewBox="0 0 24 24" fill="currentColor"><path d="M12 2.2a9.8 9.8 0 0 0-8.5 14.7L2.3 21.8l5-1.2A9.8 9.8 0 1 0 12 2.2Zm0 17.8a8 8 0 0 1-4.1-1.1l-.3-.2-3 .7.7-2.9-.2-.3A8 8 0 1 1 12 20Zm4.4-5.9c-.2-.1-1.5-.7-1.7-.8-.2-.1-.4-.1-.6.1l-.8 1c-.1.2-.3.2-.5.1-.3-.1-1.1-.4-2.1-1.3-.8-.7-1.3-1.5-1.4-1.8-.1-.2 0-.3.1-.5l.4-.5c.1-.1.1-.3.2-.4 0-.1 0-.3 0-.4-.1-.1-.6-1.4-.8-1.9-.2-.5-.4-.4-.6-.4h-.5c-.2 0-.4.1-.6.3-.2.2-.7.7-.7 1.8s.7 2.1.8 2.2c.1.1 1.4 2.2 3.5 3.1.5.2.9.4 1.2.5.5.2 1 .2 1.4.1.4-.1 1.5-.6 1.7-1.2.2-.6.2-1.1.1-1.2-.1-.1-.2-.1-.4-.2Z"/></svg>
                </span>
                <span class="mt-2 block text-xs font-bold">{{ s.name }}</span>
              </a>
            </div>
          </div>
          <form @submit.prevent="send" class="rounded-[2rem] border border-slate-200 bg-white p-7 shadow-xl dark:border-white/10 dark:bg-white/[.03]">
            <div class="grid gap-5 sm:grid-cols-2">
              <label class="text-slate-800 dark:text-slate-200">{{ t('name') }}<input v-model="form.name" required class="mt-2 w-full rounded-xl border border-slate-300 bg-slate-50 p-3 text-slate-900 outline-none placeholder:text-slate-400 focus:border-red-500 dark:border-slate-700 dark:bg-slate-900 dark:text-slate-100 dark:placeholder:text-slate-500"></label>
              <label class="text-slate-800 dark:text-slate-200">{{ t('phone') }}<input v-model="form.phone" required class="mt-2 w-full rounded-xl border border-slate-300 bg-slate-50 p-3 text-slate-900 outline-none placeholder:text-slate-400 focus:border-red-500 dark:border-slate-700 dark:bg-slate-900 dark:text-slate-100 dark:placeholder:text-slate-500"></label>
            </div>
            <label class="mt-5 block text-slate-800 dark:text-slate-200">{{ t('email') }}<input v-model="form.email" type="email" required class="mt-2 w-full rounded-xl border border-slate-300 bg-slate-50 p-3 text-slate-900 outline-none placeholder:text-slate-400 focus:border-red-500 dark:border-slate-700 dark:bg-slate-900 dark:text-slate-100 dark:placeholder:text-slate-500"></label>
            <label class="mt-5 block text-slate-800 dark:text-slate-200">{{ t('subject') }}<input v-model="form.subject" required class="mt-2 w-full rounded-xl border border-slate-300 bg-slate-50 p-3 text-slate-900 outline-none placeholder:text-slate-400 focus:border-red-500 dark:border-slate-700 dark:bg-slate-900 dark:text-slate-100 dark:placeholder:text-slate-500"></label>
            <label class="mt-5 block text-slate-800 dark:text-slate-200">{{ t('message') }}<textarea v-model="form.message" required rows="6" class="mt-2 w-full rounded-xl border border-slate-300 bg-slate-50 p-3 text-slate-900 outline-none placeholder:text-slate-400 focus:border-red-500 dark:border-slate-700 dark:bg-slate-900 dark:text-slate-100 dark:placeholder:text-slate-500"></textarea></label>
            <button class="mt-5 w-full rounded-xl bg-red-500 py-4 font-bold text-white">💬 {{ t('send') }}</button>
            <p class="mt-3 text-xs text-slate-500 dark:text-slate-400">{{ t('hint') }}</p>
          </form>
        </div>
      </section>
    </main>

    <footer class="border-t py-10 dark:border-white/10">
      <div class="mx-auto grid max-w-7xl gap-8 px-5 md:grid-cols-3">
        <div><b class="font-display text-xl">TSILAVINA<span class="text-red-500">.</span></b><p class="mt-3 text-sm text-slate-500 dark:text-slate-300">Mobile & Web Developer • Designer • Cybersecurity Explorer</p></div>
        <div>
          <b>{{ t('contact') }}</b>
          <span class="mt-3 block text-sm text-slate-500 dark:text-slate-300">
            📍 Antananarivo, Madagascar
          </span>
          <a :href="'tel:'+cleanPhone" class="mt-2 block text-sm text-slate-500 dark:text-slate-300">
            📞 +261 34 97 534 70
          </a>
          <a :href="wa" target="_blank" class="mt-2 block text-sm text-slate-600 dark:text-slate-300">
            💬 WhatsApp
          </a>
        </div>
        <div class="footer-socials">
          <b>{{ t('socials') }}</b>
          <div class="footer-social-list mt-4">
            <a v-for="s in socials" :key="s.name" :href="s.url" target="_blank" rel="noopener noreferrer" class="footer-social-item" :class="'footer-social-'+s.key" :aria-label="s.name">
              <span class="footer-social-logo" aria-hidden="true">
                <svg v-if="s.key === 'facebook'" viewBox="0 0 24 24" fill="currentColor"><path d="M14 8h3V4h-3c-3.31 0-5 1.94-5 5v3H6v4h3v8h4v-8h3.2l.8-4H13V9c0-.66.34-1 1-1Z"/></svg>
                <svg v-else-if="s.key === 'linkedin'" viewBox="0 0 24 24" fill="currentColor"><path d="M5.2 3.5A2.2 2.2 0 1 1 5.2 7.9a2.2 2.2 0 0 1 0-4.4ZM3.3 9.2h3.8V21H3.3V9.2Zm6.2 0h3.6v1.6h.1c.5-.9 1.7-1.9 3.6-1.9 3.8 0 4.5 2.5 4.5 5.8V21h-3.8v-5.6c0-1.3 0-3-1.9-3s-2.2 1.4-2.2 2.9V21H9.5V9.2Z"/></svg>
                <svg v-else-if="s.key === 'github'" viewBox="0 0 24 24" fill="currentColor"><path d="M12 2.2a9.8 9.8 0 0 0-3.1 19.1c.5.1.7-.2.7-.5v-1.9c-2.8.6-3.4-1.2-3.4-1.2-.5-1.2-1.1-1.5-1.1-1.5-.9-.6.1-.6.1-.6 1 .1 1.6 1 1.6 1 .9 1.6 2.4 1.1 3 .8.1-.7.4-1.1.7-1.3-2.2-.3-4.5-1.1-4.5-4.8 0-1.1.4-2 1-2.7-.1-.3-.4-1.3.1-2.7 0 0 .8-.3 2.8 1a9.6 9.6 0 0 1 5.1 0c2-1.3 2.8-1 2.8-1 .5 1.4.2 2.4.1 2.7.6.7 1 1.6 1 2.7 0 3.7-2.3 4.5-4.5 4.8.4.3.7 1 .7 1.9v2.8c0 .3.2.6.7.5A9.8 9.8 0 0 0 12 2.2Z"/></svg>
                <svg v-else-if="s.key === 'instagram'" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><rect x="3" y="3" width="18" height="18" rx="5"/><circle cx="12" cy="12" r="4.2"/><circle cx="17.3" cy="6.8" r="1" fill="currentColor" stroke="none"/></svg>
                <svg v-else viewBox="0 0 24 24" fill="currentColor"><path d="M12 2.2a9.8 9.8 0 0 0-8.5 14.7L2.3 21.8l5-1.2A9.8 9.8 0 1 0 12 2.2Zm0 17.8a8 8 0 0 1-4.1-1.1l-.3-.2-3 .7.7-2.9-.2-.3A8 8 0 1 1 12 20Zm4.4-5.9c-.2-.1-1.5-.7-1.7-.8-.2-.1-.4-.1-.6.1l-.8 1c-.1.2-.3.2-.5.1-.3-.1-1.1-.4-2.1-1.3-.8-.7-1.3-1.5-1.4-1.8-.1-.2 0-.3.1-.5l.4-.5c.1-.1.1-.3.2-.4 0-.1 0-.3 0-.4-.1-.1-.6-1.4-.8-1.9-.2-.5-.4-.4-.6-.4h-.5c-.2 0-.4.1-.6.3-.2.2-.7.7-.7 1.8s.7 2.1.8 2.2c.1.1 1.4 2.2 3.5 3.1.5.2.9.4 1.2.5.5.2 1 .2 1.4.1.4-.1 1.5-.6 1.7-1.2.2-.6.2-1.1.1-1.2-.1-.1-.2-.1-.4-.2Z"/></svg>
              </span>
              <span class="footer-social-name">{{ s.name }}</span>
            </a>
          </div>
        </div>
      </div>
      <div class="mx-auto mt-8 max-w-7xl border-t border-slate-200 px-5 pt-6 text-xs text-slate-500 dark:border-white/10 dark:text-slate-400">© {{ new Date().getFullYear() }} Tsilavina. {{ t('rights') }}</div>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted, nextTick } from 'vue'
import $ from 'jquery'

const lang = ref(localStorage.getItem('lang') || 'fr')
const dark = ref(localStorage.getItem('dark') !== 'false')
const menu = ref(false)
const activeSection = ref('home')
const photo = ref('/profile.jpg')
const cleanPhone = '261349753470'
const wa = 'https://wa.me/261349753470'

const nav = [
  ['home','#home'], ['about','#about'], ['formation','#formation'], ['experience','#experience'], ['competences','#competences'], ['projects','#projects'], ['contact','#contact']
]

const socials = [
  { key:'facebook', name:'Facebook', url:'https://www.facebook.com/profile.php?id=100004163671370' },
  { key:'linkedin', name:'LinkedIn', url:'https://www.linkedin.com/in/tsilavina-manase-54018629b' },
  { key:'github', name:'GitHub', url:'https://github.com/tsilavinahk' },
  { key:'instagram', name:'Instagram', url:'https://www.instagram.com/manasetsilavina?stkn=OXdzaGp4dGRkOTJ0' },
  { key:'whatsapp', name:'WhatsApp', url:wa }
]

const education = [
  {
    year:'2018',
    title:'Baccalauréat série C',
    place:'Madagascar',
    note:'Mention Assez Bien'
  },
  {
    year:'2020',
    title:'Bacc +1 en Informatique',
    place:'École Nationale d’Informatique (ENI), Fianarantsoa, Madagascar',
    note:'1 année universitaire en informatique'
  }
]

const technicalSkills = [
  { title:'Frontend', items:['React.js','Vue.js','JavaScript','HTML/CSS','TailwindCSS'] },
  { title:'Backend', items:['PHP','Symfony'] },
  { title:'Base de données & Cloud', items:['MySQL','Firebase','Firestore'] },
  { title:'Mobile', items:['Flutter'] },
  { title:'Outils', items:['Git','GitHub'] }
]

const projects = [
  { title:'Madagasikara Chine Education', type:'EdTech', visual:'EDUCATION / LMS', g:'bg-gradient-to-br from-red-600 via-slate-900 to-indigo-900', text:'Plateforme éducative pour apprenants et formateurs.' },
  { title:'Madagasikara Chine Education — Application mobile', type:'Mobile / EdTech', visual:'FLUTTER • FIREBASE', g:'bg-gradient-to-br from-sky-600 via-slate-900 to-indigo-900', text:'Développement d’une application mobile avec Flutter, Firebase et Firestore pour l’entreprise Madagasikara Chine Education.' },
  { title:'Portfolio nouvelle génération', type:'Personal Brand', visual:'DIGITAL IDENTITY', g:'bg-gradient-to-br from-fuchsia-700 via-slate-900 to-cyan-900', text:'Identité digitale moderne et premium.' },
  { title:'Dashboard Admin', type:'Product UI', visual:'COMMAND CENTER', g:'bg-gradient-to-br from-amber-600 via-slate-900 to-red-900', text:'Interface de pilotage responsive.' },
  { title:'Security Lab', type:'Learning', visual:'ETHICAL HACKING', g:'bg-gradient-to-br from-emerald-600 via-slate-900 to-blue-950', text:'Apprentissage de la cybersécurité dans un cadre légal.' }
]

const form = ref({ name:'', phone:'', email:'', subject:'', message:'' })

const D = {
  fr: {
    home:'Accueil', about:'À propos', formation:'Formation', experience:'Expérience', competences:'Compétences', projects:'Projets', contact:'Contact',
    available:'Disponible pour de nouveaux projets', hero:'Je construis des expériences', accent:'digitales mémorables.',
    intro:'Je suis MANASE Tsilavina, Mobile & Web Developer. Je transforme des idées en applications web et mobiles modernes, rapides et responsives.', see:'Voir mes projets',
    aboutTitle:'Un profil à la croisée du code et du design.', aboutText:'Mon approche associe développement, sens visuel et curiosité pour la sécurité.',
    formationTitle:'Mon parcours académique.', experienceTitle:'Mon expérience professionnelle.', experienceRole:'Développement d’applications Web', experienceType:'Expérience professionnelle', experienceText:'Développement d’applications web pour l’entreprise Madagasikara Chine Education, avec une attention portée aux interfaces, à la responsivité et aux fonctionnalités de la plateforme.',
    competencesTitle:'Mes compétences techniques.', projectTitle:'Ce que je construis.', contactTitle:'Un projet en tête ?', contactText:'Parlons de votre idée et de la meilleure façon de la transformer en produit numérique.',
    name:'Nom', phone:'Téléphone', email:'Email', subject:'Sujet', message:'Message', send:'Envoyer le message', hint:'Le bouton ouvre WhatsApp avec le message prérempli.', socials:'Réseaux sociaux', rights:'Tous droits réservés.'
  },
  en: {
    home:'Home', about:'About', formation:'Education', experience:'Experience', competences:'Skills', projects:'Projects', contact:'Contact',
    available:'Available for new projects', hero:'I build', accent:'memorable digital experiences.', intro:'I am MANASE Tsilavina, a Mobile & Web Developer. I build modern, fast and responsive web and mobile applications.', see:'View projects',
    aboutTitle:'Where code meets design.', aboutText:'My approach combines development, visual thinking and security curiosity.', formationTitle:'My academic background.', experienceTitle:'My professional experience.', experienceRole:'Web Application Development', experienceType:'Professional experience', experienceText:'Web application development for Madagasikara Chine Education, with a focus on interfaces, responsiveness and platform features.',
    competencesTitle:'My technical skills.', projectTitle:'What I build.', contactTitle:'Have a project in mind?', contactText:'Tell me about your idea and how to turn it into a digital product.',
    name:'Name', phone:'Phone', email:'Email', subject:'Subject', message:'Message', send:'Send message', hint:'The button opens WhatsApp with your message prefilled.', socials:'Social networks', rights:'All rights reserved.'
  },
  zh: {
    home:'首页', about:'关于我', formation:'教育经历', experience:'工作经验', competences:'技能', projects:'项目', contact:'联系',
    available:'目前可接新项目', hero:'打造', accent:'令人难忘的数字体验。', intro:'我是 MANASE Tsilavina，一名 Mobile & Web Developer，将想法转化为现代、快速、响应式的 Web 和移动应用。', see:'查看项目',
    aboutTitle:'代码与设计的交汇。', aboutText:'结合开发、视觉设计与安全意识，专注于清晰的界面与良好的体验。', formationTitle:'我的教育经历。', experienceTitle:'我的工作经验。', experienceRole:'Web 应用开发', experienceType:'工作经验', experienceText:'为 Madagasikara Chine Education 开发 Web 应用，重点关注界面、响应式体验和平台功能。',
    competencesTitle:'我的技术技能。', projectTitle:'我的作品。', contactTitle:'有项目想法吗？', contactText:'告诉我你的想法以及如何把它变成数字产品。',
    name:'姓名', phone:'电话', email:'邮箱', subject:'主题', message:'留言', send:'发送消息', hint:'按钮会打开 WhatsApp 并预填消息。', socials:'社交网络', rights:'版权所有。'
  }
}

function t(k) { return (D[lang.value] || D.fr)[k] || k }
function applyDark() { document.documentElement.classList.toggle('dark', dark.value); document.documentElement.style.colorScheme = dark.value ? 'dark' : 'light' }
function toggleDark() { dark.value = !dark.value; localStorage.setItem('dark', dark.value); applyDark() }
function send() {
  const f = form.value
  const msg = `Bonjour Tsilavina,%0A%0ANom: ${encodeURIComponent(f.name)}%0ATéléphone: ${encodeURIComponent(f.phone)}%0AEmail: ${encodeURIComponent(f.email)}%0ASujet: ${encodeURIComponent(f.subject)}%0A%0AMessage:%0A${encodeURIComponent(f.message)}`
  window.open(`${wa}?text=${msg}`, '_blank')
}

onMounted(async () => {
  applyDark()
  await nextTick()
  $('.reveal').css({ opacity: 0, transform: 'translateY(18px)' })
  $('.reveal').each(function(i) { $(this).delay(i * 70).animate({ opacity: 1 }, 500).css('transform','translateY(0)') })
  const sectionIds = nav.map(n => n[1].slice(1))
  const updateActiveSection = () => {
    const marker = $(window).scrollTop() + 150
    let current = 'home'
    sectionIds.forEach(id => {
      const el = document.getElementById(id)
      if (el && el.offsetTop <= marker) current = id
    })
    activeSection.value = current
  }

  $(window).on('scroll', () => {
    $('.reveal').each(function() {
      if ($(this).offset().top < $(window).scrollTop() + $(window).height() - 60) $(this).stop(true).animate({ opacity:1 }, 400).css('transform','translateY(0)')
    })
    updateActiveSection()
  })
  updateActiveSection()
})
</script>

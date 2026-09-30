```vue
<template>
  <div
    :class="{ dark }"
    class="min-h-screen overflow-x-hidden bg-slate-50 text-slate-900 transition-colors duration-500 dark:bg-slate-950 dark:text-slate-100"
  >
    <!-- =====================================================
         HEADER
    ====================================================== -->
    <header
      class="fixed inset-x-0 top-0 z-50 border-b border-slate-200/80 bg-white/90 backdrop-blur-xl dark:border-white/10 dark:bg-slate-950/90"
    >
      <nav class="mx-auto flex max-w-7xl items-center justify-between px-5 py-4">

        <a
          href="#home"
          @click="activeSection = 'home'"
          class="font-display text-xl font-bold tracking-tight"
        >
          TSILAVINA<span class="text-red-500">.</span>
        </a>

        <!-- Desktop navigation -->
        <div class="hidden gap-5 lg:flex">
          <a
            v-for="n in nav"
            :key="n[0]"
            :href="n[1]"
            @click="activeSection = n[1].slice(1)"
            :class="[
              'nav-link relative py-2 text-sm font-semibold transition duration-300 hover:text-red-500',
              activeSection === n[1].slice(1)
                ? 'text-red-500'
                : 'text-slate-700 dark:text-slate-200'
            ]"
          >
            <span>{{ t(n[0]) }}</span>

            <span
              v-if="activeSection === n[1].slice(1)"
              class="nav-active-line"
            ></span>
          </a>
        </div>

        <!-- Controls -->
        <div class="flex items-center gap-2">

          <select
            v-model="lang"
            class="rounded-xl border border-slate-300 bg-white px-2 py-2 text-xs font-semibold text-slate-900 outline-none transition hover:border-red-400 dark:border-slate-700 dark:bg-slate-900 dark:text-slate-100"
          >
            <option value="fr">FR</option>
            <option value="en">EN</option>
            <option value="zh">中文</option>
          </select>

          <button
            @click="toggleDark"
            aria-label="Changer le thème"
            class="rounded-xl border border-slate-300 px-3 py-2 text-slate-900 transition duration-300 hover:-translate-y-0.5 hover:border-red-400 hover:text-red-500 dark:border-slate-700 dark:text-slate-100"
          >
            {{ dark ? '☀' : '☾' }}
          </button>

          <button
            @click="menu = !menu"
            aria-label="Menu"
            class="rounded-xl border border-slate-300 px-3 py-2 transition hover:border-red-400 hover:text-red-500 dark:border-slate-700 lg:hidden"
          >
            {{ menu ? '✕' : '☰' }}
          </button>
        </div>
      </nav>

      <!-- Mobile menu -->
      <div
        v-if="menu"
        class="mobile-menu border-t border-slate-200 bg-white p-4 dark:border-white/10 dark:bg-slate-950 lg:hidden"
      >
        <a
          v-for="n in nav"
          :key="n[0]"
          :href="n[1]"
          @click="
            activeSection = n[1].slice(1);
            menu = false
          "
          :class="[
            'relative mb-1 block rounded-xl p-3 font-semibold text-slate-700 transition duration-300 hover:bg-slate-100 hover:text-red-500 dark:text-slate-200 dark:hover:bg-white/5',
            activeSection === n[1].slice(1)
              ? 'bg-red-500/5 text-red-500 dark:bg-red-500/10 dark:text-red-300'
              : ''
          ]"
        >
          {{ t(n[0]) }}

          <span
            v-if="activeSection === n[1].slice(1)"
            class="nav-active-line-mobile"
          ></span>
        </a>
      </div>
    </header>


    <!-- =====================================================
         MAIN
    ====================================================== -->
    <main id="home">

      <!-- ===================================================
           HERO
      ==================================================== -->
      <section class="grid-glow min-h-screen pt-28">

        <div
          class="mx-auto grid max-w-7xl gap-12 px-5 py-20 lg:grid-cols-2 lg:items-center"
        >

          <div>

            <span
              class="reveal inline-block rounded-full border border-red-300 bg-red-50 px-4 py-2 text-sm font-semibold text-red-600 dark:bg-red-500/10 dark:text-red-300"
            >
              ● {{ t('available') }}
            </span>

            <p
              class="reveal mt-6 text-sm font-bold uppercase tracking-[.25em] text-slate-500 dark:text-slate-300"
              style="--reveal-delay: 80ms"
            >
              Mobile & Web • Design • Cybersecurity
            </p>

            <h1
              class="reveal mt-4 text-5xl font-bold leading-none tracking-tight sm:text-7xl"
              style="--reveal-delay: 160ms"
            >
              {{ t('hero') }}
              <span class="text-red-500">
                {{ t('accent') }}
              </span>
            </h1>

            <p
              class="reveal mt-7 max-w-2xl text-lg leading-8 text-slate-600 dark:text-slate-400"
              style="--reveal-delay: 240ms"
            >
              {{ t('intro') }}
            </p>

            <div
              class="reveal mt-9 flex flex-col gap-3 sm:flex-row"
              style="--reveal-delay: 320ms"
            >
              <a
                href="#projects"
                class="premium-button rounded-full bg-red-500 px-7 py-3.5 text-center font-bold text-white shadow-lg shadow-red-500/20"
              >
                {{ t('see') }}
              </a>

              <a
                href="#contact"
                class="premium-button rounded-full border border-slate-300 px-7 py-3.5 text-center font-bold text-slate-900 dark:border-slate-700 dark:text-slate-100"
              >
                {{ t('contact') }}
              </a>
            </div>

          </div>


          <!-- Profile -->
          <div
            class="reveal premium-card mx-auto w-full max-w-md rounded-[2rem] border border-slate-200 bg-white p-3 shadow-2xl dark:border-white/10 dark:bg-white/[.03]"
            style="--reveal-delay: 180ms"
          >
            <div class="profile-image-wrapper overflow-hidden rounded-[1.5rem]">
              <img
                :src="photo"
                @error="photo = '/profile-placeholder.svg'"
                alt="Tsilavina"
                class="aspect-[4/5] w-full rounded-[1.5rem] object-cover"
              >
            </div>
          </div>

        </div>
      </section>


      <!-- ===================================================
           ABOUT
      ==================================================== -->
      <section
        id="about"
        class="border-t py-24 dark:border-white/5"
      >
        <div class="mx-auto max-w-7xl px-5">

          <p class="text-sm font-bold uppercase tracking-[.25em] text-red-500">
            {{ t('about') }}
          </p>

          <h2
            class="reveal mt-3 text-4xl font-bold tracking-tight sm:text-5xl"
          >
            {{ t('aboutTitle') }}
          </h2>

          <p
            class="reveal mt-5 max-w-3xl text-lg leading-8 text-slate-600 dark:text-slate-400"
            style="--reveal-delay: 100ms"
          >
            {{ t('aboutText') }}
          </p>

        </div>
      </section>


      <!-- ===================================================
           FORMATION
      ==================================================== -->
      <section
        id="formation"
        class="border-t bg-slate-100 py-24 dark:border-white/5 dark:bg-slate-900/40"
      >
        <div class="mx-auto max-w-7xl px-5">

          <p class="text-sm font-bold uppercase tracking-[.25em] text-red-500">
            {{ t('formation') }}
          </p>

          <h2
            class="reveal mt-3 text-4xl font-bold tracking-tight sm:text-5xl"
          >
            {{ t('formationTitle') }}
          </h2>

          <div class="mt-10 grid gap-6 md:grid-cols-2">

            <article
              v-for="(item, index) in education"
              :key="item.year"
              class="reveal premium-card rounded-3xl border border-slate-200 bg-white p-7 shadow-sm dark:border-white/10 dark:bg-slate-950"
              :style="{ '--reveal-delay': `${index * 120}ms` }"
            >

              <span
                class="relative z-10 inline-flex rounded-full bg-red-500/10 px-4 py-2 text-sm font-bold text-red-600 dark:text-red-300"
              >
                {{ item.year }}
              </span>

              <h3 class="relative z-10 mt-5 text-2xl font-bold">
                {{ item.title }}
              </h3>

              <p class="relative z-10 mt-3 leading-7 text-slate-600 dark:text-slate-300">
                {{ item.place }}
              </p>

              <p
                v-if="item.note"
                class="relative z-10 mt-2 font-semibold text-red-500"
              >
                {{ item.note }}
              </p>

            </article>

          </div>
        </div>
      </section>


      <!-- ===================================================
           EXPERIENCE
      ==================================================== -->
      <section
        id="experience"
        class="border-t py-24 dark:border-white/5"
      >
        <div class="mx-auto max-w-7xl px-5">

          <p class="text-sm font-bold uppercase tracking-[.25em] text-red-500">
            {{ t('experience') }}
          </p>

          <h2
            class="reveal mt-3 text-4xl font-bold tracking-tight sm:text-5xl"
          >
            {{ t('experienceTitle') }}
          </h2>

          <article
            class="reveal premium-card mt-10 rounded-3xl border border-slate-200 bg-white p-8 shadow-sm dark:border-white/10 dark:bg-slate-900/50"
            style="--reveal-delay: 120ms"
          >

            <div class="relative z-10 flex flex-col gap-3 sm:flex-row sm:items-center sm:justify-between">

              <h3 class="text-2xl font-bold">
                {{ t('experienceRole') }}
              </h3>

              <span
                class="inline-flex w-fit rounded-full bg-red-500/10 px-4 py-2 text-sm font-semibold text-red-600 dark:text-red-300"
              >
                {{ t('experienceType') }}
              </span>

            </div>

            <p class="relative z-10 mt-4 text-lg font-semibold">
              Madagasikara Chine Education
            </p>

            <p
              class="relative z-10 mt-4 max-w-3xl leading-8 text-slate-600 dark:text-slate-300"
            >
              {{ t('experienceText') }}
            </p>

          </article>

        </div>
      </section>


      <!-- ===================================================
           COMPÉTENCES
      ==================================================== -->
      <section
        id="competences"
        class="border-t py-24 dark:border-white/5"
      >
        <div class="mx-auto max-w-7xl px-5">

          <p class="text-sm font-bold uppercase tracking-[.25em] text-red-500">
            {{ t('competences') }}
          </p>

          <h2
            class="reveal mt-3 text-4xl font-bold tracking-tight sm:text-5xl"
          >
            {{ t('competencesTitle') }}
          </h2>

          <div class="mt-10 grid gap-6 sm:grid-cols-2 lg:grid-cols-4">

            <div
              v-for="(group, index) in technicalSkills"
              :key="group.title"
              class="reveal premium-card rounded-3xl border border-slate-200 bg-white p-7 dark:border-white/10 dark:bg-slate-900/50"
              :style="{ '--reveal-delay': `${index * 100}ms` }"
            >

              <div class="relative z-10">

                <div
                  class="mb-5 flex h-12 w-12 items-center justify-center rounded-2xl bg-red-500/10 text-xl text-red-500"
                >
                  <span>✦</span>
                </div>

                <h3 class="text-xl font-bold">
                  {{ group.title }}
                </h3>

                <ul class="mt-5 space-y-3">

                  <li
                    v-for="skill in group.items"
                    :key="skill"
                    class="flex items-center gap-2 text-slate-600 dark:text-slate-300"
                  >
                    <span class="text-red-500">●</span>
                    {{ skill }}
                  </li>

                </ul>

              </div>

            </div>

          </div>
        </div>
      </section>


      <!-- ===================================================
           PROJETS
      ==================================================== -->
      <section
        id="projects"
        class="border-t bg-slate-100 py-24 dark:border-white/5 dark:bg-slate-900/40"
      >
        <div class="mx-auto max-w-7xl px-5">

          <p class="text-sm font-bold uppercase tracking-[.25em] text-red-500">
            {{ t('projects') }}
          </p>

          <h2
            class="reveal mt-3 text-4xl font-bold tracking-tight sm:text-5xl"
          >
            {{ t('projectTitle') }}
          </h2>

          <div class="mt-10 grid gap-6 md:grid-cols-2">

            <article
              v-for="(p, index) in projects"
              :key="p.title"
              class="reveal premium-card overflow-hidden rounded-3xl border border-slate-200 bg-white dark:border-white/10 dark:bg-slate-950"
              :style="{ '--reveal-delay': `${index * 110}ms` }"
            >

              <div
                :class="p.g"
                class="project-visual relative aspect-video overflow-hidden p-7"
              >

                <div class="relative z-10">

                  <span
                    class="inline-flex rounded-full bg-black/25 px-3 py-2 text-xs font-bold text-white backdrop-blur-sm"
                  >
                    {{ p.type }}
                  </span>

                  <p class="mt-20 text-3xl font-bold tracking-tight text-white">
                    {{ p.visual }}
                  </p>

                </div>

              </div>

              <div class="relative z-10 p-7">

                <h3 class="text-2xl font-bold">
                  {{ p.title }}
                </h3>

                <p class="mt-3 leading-7 text-slate-600 dark:text-slate-300">
                  {{ p.text }}
                </p>

              </div>

            </article>

          </div>
        </div>
      </section>


      <!-- ===================================================
           CONTACT
      ==================================================== -->
      <section
        id="contact"
        class="border-t py-24 dark:border-white/5"
      >
        <div class="mx-auto grid max-w-7xl gap-12 px-5 lg:grid-cols-2">

          <!-- Informations -->
          <div>

            <p class="text-sm font-bold uppercase tracking-[.25em] text-red-500">
              {{ t('contact') }}
            </p>

            <h2
              class="reveal mt-3 text-4xl font-bold tracking-tight sm:text-5xl"
            >
              {{ t('contactTitle') }}
            </h2>

            <p
              class="reveal mt-5 text-lg leading-8 text-slate-600 dark:text-slate-300"
              style="--reveal-delay: 100ms"
            >
              {{ t('contactText') }}
            </p>


            <!-- Localisation -->
            <div
              class="reveal premium-card mt-8 rounded-2xl border border-slate-200 bg-white p-4 font-semibold text-slate-800 dark:border-slate-700 dark:bg-slate-900 dark:text-slate-100"
              style="--reveal-delay: 150ms"
            >
              <span class="relative z-10">
                📍 Antananarivo, Madagascar
              </span>
            </div>


            <!-- Téléphone -->
            <a
              :href="'tel:' + cleanPhone"
              class="reveal premium-card mt-3 block rounded-2xl border border-slate-200 bg-white p-4 font-semibold text-slate-800 dark:border-slate-700 dark:bg-slate-900 dark:text-slate-100"
              style="--reveal-delay: 200ms"
            >
              <span class="relative z-10">
                📞 +261 34 97 534 70
              </span>
            </a>


            <!-- WhatsApp -->
            <a
              :href="wa"
              target="_blank"
              rel="noopener noreferrer"
              class="reveal premium-card mt-3 block rounded-2xl border border-slate-200 bg-white p-4 font-semibold text-slate-800 dark:border-slate-700 dark:bg-slate-900 dark:text-slate-100"
              style="--reveal-delay: 250ms"
            >
              <span class="relative z-10">
                💬 WhatsApp
              </span>
            </a>


            <!-- Réseaux sociaux -->
            <div class="mt-6 grid grid-cols-2 gap-3 sm:grid-cols-3 lg:grid-cols-5">

              <a
                v-for="(s, index) in socials"
                :key="s.name"
                :href="s.url"
                target="_blank"
                rel="noopener noreferrer"
                class="reveal premium-card social social-card group rounded-2xl border border-slate-200 bg-white p-3 text-center text-slate-700 shadow-sm dark:border-white/10 dark:bg-slate-900/70 dark:text-slate-200"
                :style="{ '--reveal-delay': `${300 + index * 70}ms` }"
              >

                <span
                  class="social-icon relative z-10 mx-auto"
                  :class="'social-' + s.key"
                  aria-hidden="true"
                >

                  <svg
                    v-if="s.key === 'facebook'"
                    viewBox="0 0 24 24"
                    fill="currentColor"
                  >
                    <path d="M14 8h3V4h-3c-3.31 0-5 1.94-5 5v3H6v4h3v8h4v-8h3.2l.8-4H13V9c0-.66.34-1 1-1Z"/>
                  </svg>

                  <svg
                    v-else-if="s.key === 'linkedin'"
                    viewBox="0 0 24 24"
                    fill="currentColor"
                  >
                    <path d="M5.2 3.5A2.2 2.2 0 1 1 5.2 7.9a2.2 2.2 0 0 1 0-4.4ZM3.3 9.2h3.8V21H3.3V9.2Zm6.2 0h3.6v1.6h.1c.5-.9 1.7-1.9 3.6-1.9 3.8 0 4.5 2.5 4.5 5.8V21h-3.8v-5.6c0-1.3 0-3-1.9-3s-2.2 1.4-2.2 2.9V21H9.5V9.2Z"/>
                  </svg>

                  <svg
                    v-else-if="s.key === 'github'"
                    viewBox="0 0 24 24"
                    fill="currentColor"
                  >
                    <path d="M12 2.2a9.8 9.8 0 0 0-3.1 19.1c.5.1.7-.2.7-.5v-1.9c-2.8.6-3.4-1.2-3.4-1.2-.5-1.2-1.1-1.5-1.1-1.5-.9-.6.1-.6.1-.6 1 .1 1.6 1 1.6 1 .9 1.6 2.4 1.1 3 .8.1-.7.4-1.1.7-1.3-2.2-.3-4.5-1.1-4.5-4.8 0-1.1.4-2 1-2.7-.1-.3-.4-1.3.1-2.7 0 0 .8-.3 2.8 1a9.6 9.6 0 0 1 5.1 0c2-1.3 2.8-1 2.8-1 .5 1.4.2 2.4.1 2.7.6.7 1 1.6 1 2.7 0 3.7-2.3 4.5-4.5 4.8.4.3.7 1 .7 1.9v2.8c0 .3.2.6.7.5A9.8 9.8 0 0 0 12 2.2Z"/>
                  </svg>

                  <svg
                    v-else-if="s.key === 'instagram'"
                    viewBox="0 0 24 24"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="1.8"
                  >
                    <rect x="3" y="3" width="18" height="18" rx="5"/>
                    <circle cx="12" cy="12" r="4.2"/>
                    <circle cx="17.3" cy="6.8" r="1" fill="currentColor" stroke="none"/>
                  </svg>

                  <svg
                    v-else
                    viewBox="0 0 24 24"
                    fill="currentColor"
                  >
                    <path d="M12 2.2a9.8 9.8 0 0 0-8.5 14.7L2.3 21.8l5-1.2A9.8 9.8 0 1 0 12 2.2Zm0 17.8a8 8 0 0 1-4.1-1.1l-.3-.2-3 .7.7-2.9-.2-.3A8 8 0 1 1 12 20Zm4.4-5.9c-.2-.1-1.5-.7-1.7-.8-.2-.1-.4-.1-.6.1l-.8 1c-.1.2-.3.2-.5.1-.3-.1-1.1-.4-2.1-1.3-.8-.7-1.3-1.5-1.4-1.8-.1-.2 0-.3.1-.5l.4-.5c.1-.1.1-.3.2-.4 0-.1 0-.3 0-.4-.1-.1-.6-1.4-.8-1.9-.2-.5-.4-.4-.6-.4h-.5c-.2 0-.4.1-.6.3-.2.2-.7.7-.7 1.8s.7 2.1.8 2.2c.1.1 1.4 2.2 3.5 3.1.5.2.9.4 1.2.5.5.2 1 .2 1.4.1.4-.1 1.5-.6 1.7-1.2.2-.6.2-1.1.1-1.2-.1-.1-.2-.1-.4-.2Z"/>
                  </svg>

                </span>

                <span class="relative z-10 mt-2 block text-xs font-bold">
                  {{ s.name }}
                </span>

              </a>

            </div>

          </div>


          <!-- Formulaire -->
          <form
            @submit.prevent="send"
            class="reveal premium-card rounded-[2rem] border border-slate-200 bg-white p-7 shadow-xl dark:border-white/10 dark:bg-white/[.03]"
            style="--reveal-delay: 150ms"
          >

            <div class="relative z-10">

              <div class="grid gap-5 sm:grid-cols-2">

                <label class="text-slate-800 dark:text-slate-200">
                  {{ t('name') }}

                  <input
                    v-model="form.name"
                    required
                    class="mt-2 w-full rounded-xl border border-slate-300 bg-slate-50 p-3 text-slate-900 outline-none transition focus:border-red-500 focus:ring-2 focus:ring-red-500/10 dark:border-slate-700 dark:bg-slate-900 dark:text-slate-100"
                  >
                </label>

                <label class="text-slate-800 dark:text-slate-200">
                  {{ t('phone') }}

                  <input
                    v-model="form.phone"
                    required
                    class="mt-2 w-full rounded-xl border border-slate-300 bg-slate-50 p-3 text-slate-900 outline-none transition focus:border-red-500 focus:ring-2 focus:ring-red-500/10 dark:border-slate-700 dark:bg-slate-900 dark:text-slate-100"
                  >
                </label>

              </div>


              <label class="mt-5 block text-slate-800 dark:text-slate-200">
                {{ t('email') }}

                <input
                  v-model="form.email"
                  type="email"
                  required
                  class="mt-2 w-full rounded-xl border border-slate-300 bg-slate-50 p-3 text-slate-900 outline-none transition focus:border-red-500 focus:ring-2 focus:ring-red-500/10 dark:border-slate-700 dark:bg-slate-900 dark:text-slate-100"
                >
              </label>


              <label class="mt-5 block text-slate-800 dark:text-slate-200">
                {{ t('subject') }}

                <input
                  v-model="form.subject"
                  required
                  class="mt-2 w-full rounded-xl border border-slate-300 bg-slate-50 p-3 text-slate-900 outline-none transition focus:border-red-500 focus:ring-2 focus:ring-red-500/10 dark:border-slate-700 dark:bg-slate-900 dark:text-slate-100"
                >
              </label>


              <label class="mt-5 block text-slate-800 dark:text-slate-200">
                {{ t('message') }}

                <textarea
                  v-model="form.message"
                  required
                  rows="6"
                  class="mt-2 w-full resize-none rounded-xl border border-slate-300 bg-slate-50 p-3 text-slate-900 outline-none transition focus:border-red-500 focus:ring-2 focus:ring-red-500/10 dark:border-slate-700 dark:bg-slate-900 dark:text-slate-100"
                ></textarea>
              </label>


              <button
                class="premium-button mt-5 w-full rounded-xl bg-red-500 py-4 font-bold text-white shadow-lg shadow-red-500/20"
              >
                💬 {{ t('send') }}
              </button>

              <p class="mt-3 text-xs text-slate-500 dark:text-slate-400">
                {{ t('hint') }}
              </p>

            </div>

          </form>

        </div>
      </section>

    </main>


    <!-- =====================================================
         FOOTER
    ====================================================== -->
    <footer class="border-t py-10 dark:border-white/10">

      <div class="mx-auto grid max-w-7xl gap-8 px-5 md:grid-cols-3">

        <div>
          <b class="font-display text-xl">
            TSILAVINA<span class="text-red-500">.</span>
          </b>

          <p class="mt-3 text-sm text-slate-500 dark:text-slate-300">
            Mobile & Web Developer • Designer • Cybersecurity Explorer
          </p>
        </div>


        <div>

          <b>{{ t('contact') }}</b>

          <span class="mt-3 block text-sm text-slate-500 dark:text-slate-300">
            📍 Antananarivo, Madagascar
          </span>

          <a
            :href="'tel:' + cleanPhone"
            class="mt-2 block text-sm text-slate-500 transition hover:text-red-500 dark:text-slate-300"
          >
            📞 +261 34 97 534 70
          </a>

          <a
            :href="wa"
            target="_blank"
            rel="noopener noreferrer"
            class="mt-2 block text-sm text-slate-600 transition hover:text-red-500 dark:text-slate-300"
          >
            💬 WhatsApp
          </a>

        </div>


        <div class="footer-socials">

          <b>{{ t('socials') }}</b>

          <div class="footer-social-list mt-4">

            <a
              v-for="s in socials"
              :key="s.name"
              :href="s.url"
              target="_blank"
              rel="noopener noreferrer"
              class="footer-social-item"
              :class="'footer-social-' + s.key"
              :aria-label="s.name"
            >

              <span
                class="footer-social-logo"
                aria-hidden="true"
              >

                <svg
                  v-if="s.key === 'facebook'"
                  viewBox="0 0 24 24"
                  fill="currentColor"
                >
                  <path d="M14 8h3V4h-3c-3.31 0-5 1.94-5 5v3H6v4h3v8h4v-8h3.2l.8-4H13V9c0-.66.34-1 1-1Z"/>
                </svg>

                <svg
                  v-else-if="s.key === 'linkedin'"
                  viewBox="0 0 24 24"
                  fill="currentColor"
                >
                  <path d="M5.2 3.5A2.2 2.2 0 1 1 5.2 7.9a2.2 2.2 0 0 1 0-4.4ZM3.3 9.2h3.8V21H3.3V9.2Zm6.2 0h3.6v1.6h.1c.5-.9 1.7-1.9 3.6-1.9 3.8 0 4.5 2.5 4.5 5.8V21h-3.8v-5.6c0-1.3 0-3-1.9-3s-2.2 1.4-2.2 2.9V21H9.5V9.2Z"/>
                </svg>

                <svg
                  v-else-if="s.key === 'github'"
                  viewBox="0 0 24 24"
                  fill="currentColor"
                >
                  <path d="M12 2.2a9.8 9.8 0 0 0-3.1 19.1c.5.1.7-.2.7-.5v-1.9c-2.8.6-3.4-1.2-3.4-1.2-.5-1.2-1.1-1.5-1.1-1.5-.9-.6.1-.6.1-.6 1 .1 1.6 1 1.6 1 .9 1.6 2.4 1.1 3 .8.1-.7.4-1.1.7-1.3-2.2-.3-4.5-1.1-4.5-4.8 0-1.1.4-2 1-2.7-.1-.3-.4-1.3.1-2.7 0 0 .8-.3 2.8 1a9.6 9.6 0 0 1 5.1 0c2-1.3 2.8-1 2.8-1 .5 1.4.2 2.4.1 2.7.6.7 1 1.6 1 2.7 0 3.7-2.3 4.5-4.5 4.8.4.3.7 1 .7 1.9v2.8c0 .3.2.6.7.5A9.8 9.8 0 0 0 12 2.2Z"/>
                </svg>

                <svg
                  v-else-if="s.key === 'instagram'"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="1.8"
                >
                  <rect x="3" y="3" width="18" height="18" rx="5"/>
                  <circle cx="12" cy="12" r="4.2"/>
                  <circle cx="17.3" cy="6.8" r="1" fill="currentColor" stroke="none"/>
                </svg>

                <svg
                  v-else
                  viewBox="0 0 24 24"
                  fill="currentColor"
                >
                  <path d="M12 2.2a9.8 9.8 0 0 0-8.5 14.7L2.3 21.8l5-1.2A9.8 9.8 0 1 0 12 2.2Zm0 17.8a8 8 0 0 1-4.1-1.1l-.3-.2-3 .7.7-2.9-.2-.3A8 8 0 1 1 12 20Zm4.4-5.9c-.2-.1-1.5-.7-1.7-.8-.2-.1-.4-.1-.6.1l-.8 1c-.1.2-.3.2-.5.1-.3-.1-1.1-.4-2.1-1.3-.8-.7-1.3-1.5-1.4-1.8-.1-.2 0-.3.1-.5l.4-.5c.1-.1.1-.3.2-.4 0-.1 0-.3 0-.4-.1-.1-.6-1.4-.8-1.9-.2-.5-.4-.4-.6-.4h-.5c-.2 0-.4.1-.6.3-.2.2-.7.7-.7 1.8s.7 2.1.8 2.2c.1.1 1.4 2.2 3.5 3.1.5.2.9.4 1.2.1.4-.1 1.5-.6 1.7-1.2.2-.6.2-1.1.1-1.2-.1-.1-.2-.1-.4-.2Z"/>
                </svg>

              </span>

              <span class="footer-social-name">
                {{ s.name }}
              </span>

            </a>

          </div>
        </div>

      </div>


      <div
        class="mx-auto mt-8 max-w-7xl border-t border-slate-200 px-5 pt-6 text-xs text-slate-500 dark:border-white/10 dark:text-slate-400"
      >
        © {{ new Date().getFullYear() }} Tsilavina. {{ t('rights') }}
      </div>

    </footer>

  </div>
</template>


<script setup>
import { ref, onMounted, nextTick } from 'vue'
import $ from 'jquery'


/* =========================================================
   ÉTAT
========================================================= */

const lang = ref(localStorage.getItem('lang') || 'fr')
const dark = ref(localStorage.getItem('dark') !== 'false')
const menu = ref(false)
const activeSection = ref('home')

const photo = ref('/profile.jpg')

const cleanPhone = '261349753470'
const wa = 'https://wa.me/261349753470'


/* =========================================================
   NAVIGATION
========================================================= */

const nav = [
  ['home', '#home'],
  ['about', '#about'],
  ['formation', '#formation'],
  ['experience', '#experience'],
  ['competences', '#competences'],
  ['projects', '#projects'],
  ['contact', '#contact']
]


/* =========================================================
   RÉSEAUX SOCIAUX
========================================================= */

const socials = [
  {
    key: 'facebook',
    name: 'Facebook',
    url: 'https://www.facebook.com/profile.php?id=100004163671370'
  },
  {
    key: 'linkedin',
    name: 'LinkedIn',
    url: 'https://www.linkedin.com/in/tsilavina-manase-54018629b'
  },
  {
    key: 'github',
    name: 'GitHub',
    url: 'https://github.com/tsilavinahk'
  },
  {
    key: 'instagram',
    name: 'Instagram',
    url: 'https://www.instagram.com/manasetsilavina?stkn=OXdzaGp4dGRkOTJ0'
  },
  {
    key: 'whatsapp',
    name: 'WhatsApp',
    url: wa
  }
]


/* =========================================================
   FORMATION
========================================================= */

const education = [
  {
    year: '2018',
    title: 'Baccalauréat série C',
    place: 'Madagascar',
    note: 'Mention Assez Bien'
  },
  {
    year: '2020',
    title: 'Bacc +1 en Informatique',
    place: 'École Nationale d’Informatique (ENI), Fianarantsoa, Madagascar',
    note: '1 année universitaire en informatique'
  }
]


/* =========================================================
   COMPÉTENCES
========================================================= */

const technicalSkills = [
  {
    title: 'Frontend',
    items: [
      'React.js',
      'Vue.js',
      'JavaScript',
      'HTML/CSS',
      'TailwindCSS'
    ]
  },
  {
    title: 'Backend',
    items: [
      'PHP',
      'Symfony'
    ]
  },
  {
    title: 'Base de données & Cloud',
    items: [
      'MySQL',
      'Firebase',
      'Firestore'
    ]
  },
  {
    title: 'Mobile',
    items: [
      'Flutter'
    ]
  },
  {
    title: 'Outils',
    items: [
      'Git',
      'GitHub'
    ]
  }
]


/* =========================================================
   PROJETS
========================================================= */

const projects = [
  {
    title: 'Madagasikara Chine Education',
    type: 'EdTech',
    visual: 'EDUCATION / LMS',
    g: 'bg-gradient-to-br from-red-600 via-slate-900 to-indigo-900',
    text: 'Plateforme éducative pour apprenants et formateurs.'
  },
  {
    title: 'Madagasikara Chine Education — Application mobile',
    type: 'Mobile / EdTech',
    visual: 'FLUTTER • FIREBASE',
    g: 'bg-gradient-to-br from-sky-600 via-slate-900 to-indigo-900',
    text: 'Développement d’une application mobile avec Flutter, Firebase et Firestore pour l’entreprise Madagasikara Chine Education.'
  },
  {
    title: 'Portfolio nouvelle génération',
    type: 'Personal Brand',
    visual: 'DIGITAL IDENTITY',
    g: 'bg-gradient-to-br from-fuchsia-700 via-slate-900 to-cyan-900',
    text: 'Identité digitale moderne et premium.'
  },
  {
    title: 'Dashboard Admin',
    type: 'Product UI',
    visual: 'COMMAND CENTER',
    g: 'bg-gradient-to-br from-amber-600 via-slate-900 to-red-900',
    text: 'Interface de pilotage responsive.'
  },
  {
    title: 'Security Lab',
    type: 'Learning',
    visual: 'ETHICAL HACKING',
    g: 'bg-gradient-to-br from-emerald-600 via-slate-900 to-blue-950',
    text: 'Apprentissage de la cybersécurité dans un cadre légal.'
  }
]


/* =========================================================
   FORMULAIRE
========================================================= */

const form = ref({
  name: '',
  phone: '',
  email: '',
  subject: '',
  message: ''
})


/* =========================================================
   TRADUCTIONS
========================================================= */

const D = {

  fr: {
    home: 'Accueil',
    about: 'À propos',
    formation: 'Formation',
    experience: 'Expérience',
    competences: 'Compétences',
    projects: 'Projets',
    contact: 'Contact',

    available: 'Disponible pour de nouveaux projets',

    hero: 'Je construis des expériences',
    accent: 'digitales mémorables.',

    intro:
      'Je suis MANASE Tsilavina, Mobile & Web Developer. Je transforme des idées en applications web et mobiles modernes, rapides et responsives.',

    see: 'Voir mes projets',

    aboutTitle:
      'Un profil à la croisée du code et du design.',

    aboutText:
      'Mon approche associe développement, sens visuel et curiosité pour la sécurité.',

    formationTitle:
      'Mon parcours académique.',

    experienceTitle:
      'Mon expérience professionnelle.',

    experienceRole:
      'Développement d’applications Web',

    experienceType:
      'Expérience professionnelle',

    experienceText:
      'Développement d’applications web pour l’entreprise Madagasikara Chine Education, avec une attention portée aux interfaces, à la responsivité et aux fonctionnalités de la plateforme.',

    competencesTitle:
      'Mes compétences techniques.',

    projectTitle:
      'Ce que je construis.',

    contactTitle:
      'Un projet en tête ?',

    contactText:
      'Parlons de votre idée et de la meilleure façon de la transformer en produit numérique.',

    name: 'Nom',
    phone: 'Téléphone',
    email: 'Email',
    subject: 'Sujet',
    message: 'Message',

    send: 'Envoyer le message',

    hint:
      'Le bouton ouvre WhatsApp avec le message prérempli.',

    socials:
      'Réseaux sociaux',

    rights:
      'Tous droits réservés.'
  },


  en: {
    home: 'Home',
    about: 'About',
    formation: 'Education',
    experience: 'Experience',
    competences: 'Skills',
    projects: 'Projects',
    contact: 'Contact',

    available: 'Available for new projects',

    hero: 'I build',
    accent: 'memorable digital experiences.',

    intro:
      'I am MANASE Tsilavina, a Mobile & Web Developer. I build modern, fast and responsive web and mobile applications.',

    see: 'View projects',

    aboutTitle:
      'Where code meets design.',

    aboutText:
      'My approach combines development, visual thinking and security curiosity.',

    formationTitle:
      'My academic background.',

    experienceTitle:
      'My professional experience.',

    experienceRole:
      'Web Application Development',

    experienceType:
      'Professional experience',

    experienceText:
      'Web application development for Madagasikara Chine Education, with a focus on interfaces, responsiveness and platform features.',

    competencesTitle:
      'My technical skills.',

    projectTitle:
      'What I build.',

    contactTitle:
      'Have a project in mind?',

    contactText:
      'Tell me about your idea and how to turn it into a digital product.',

    name: 'Name',
    phone: 'Phone',
    email: 'Email',
    subject: 'Subject',
    message: 'Message',

    send: 'Send message',

    hint:
      'The button opens WhatsApp with your message prefilled.',

    socials:
      'Social networks',

    rights:
      'All rights reserved.'
  },


  zh: {
    home: '首页',
    about: '关于我',
    formation: '教育经历',
    experience: '工作经验',
    competences: '技能',
    projects: '项目',
    contact: '联系',

    available: '目前可接新项目',

    hero: '打造',
    accent: '令人难忘的数字体验。',

    intro:
      '我是 MANASE Tsilavina，一名 Mobile & Web Developer，将想法转化为现代、快速、响应式的 Web 和移动应用。',

    see: '查看项目',

    aboutTitle:
      '代码与设计的交汇。',

    aboutText:
      '结合开发、视觉设计与安全意识，专注于清晰的界面与良好的体验。',

    formationTitle:
      '我的教育经历。',

    experienceTitle:
      '我的工作经验。',

    experienceRole:
      'Web 应用开发',

    experienceType:
      '工作经验',

    experienceText:
      '为 Madagasikara Chine Education 开发 Web 应用，重点关注界面、响应式体验和平台功能。',

    competencesTitle:
      '我的技术技能。',

    projectTitle:
      '我的作品。',

    contactTitle:
      '有项目想法吗？',

    contactText:
      '告诉我你的想法以及如何把它变成数字产品。',

    name: '姓名',
    phone: '电话',
    email: '邮箱',
    subject: '主题',
    message: '留言',

    send: '发送消息',

    hint:
      '按钮会打开 WhatsApp 并预填消息。',

    socials:
      '社交网络',

    rights:
      '版权所有。'
  }

}


/* =========================================================
   TRADUCTION
========================================================= */

function t(key) {
  return (D[lang.value] || D.fr)[key] || key
}


/* =========================================================
   MODE SOMBRE
========================================================= */

function applyDark() {
  document.documentElement.classList.toggle(
    'dark',
    dark.value
  )

  document.documentElement.style.colorScheme =
    dark.value ? 'dark' : 'light'
}


function toggleDark() {
  dark.value = !dark.value

  localStorage.setItem(
    'dark',
    dark.value
  )

  applyDark()
}


/* =========================================================
   WHATSAPP
========================================================= */

function send() {

  const f = form.value

  const msg =
    `Bonjour Tsilavina,%0A%0A` +
    `Nom: ${encodeURIComponent(f.name)}%0A` +
    `Téléphone: ${encodeURIComponent(f.phone)}%0A` +
    `Email: ${encodeURIComponent(f.email)}%0A` +
    `Sujet: ${encodeURIComponent(f.subject)}%0A%0A` +
    `Message:%0A${encodeURIComponent(f.message)}`

  window.open(
    `${wa}?text=${msg}`,
    '_blank'
  )
}


/* =========================================================
   MONTAGE
========================================================= */

onMounted(async () => {

  applyDark()

  await nextTick()


  /* -------------------------------------------------------
     REVEAL AU SCROLL
  ------------------------------------------------------- */

  const revealElements =
    document.querySelectorAll('.reveal')


  const observer =
    new IntersectionObserver(
      (entries) => {

        entries.forEach((entry) => {

          if (entry.isIntersecting) {

            entry.target.classList.add(
              'is-visible'
            )

            observer.unobserve(
              entry.target
            )

          }

        })

      },
      {
        threshold: 0.12,
        rootMargin: '0px 0px -60px 0px'
      }
    )


  revealElements.forEach((element) => {
    observer.observe(element)
  })


  /* -------------------------------------------------------
     LUMIÈRE QUI SUIT LA SOURIS
  ------------------------------------------------------- */

  document
    .querySelectorAll('.premium-card')
    .forEach((card) => {

      card.addEventListener(
        'mousemove',
        (event) => {

          const rect =
            card.getBoundingClientRect()

          const x =
            event.clientX - rect.left

          const y =
            event.clientY - rect.top

          card.style.setProperty(
            '--mouse-x',
            `${x}px`
          )

          card.style.setProperty(
            '--mouse-y',
            `${y}px`
          )

        }
      )


      card.addEventListener(
        'mouseleave',
        () => {

          card.style.setProperty(
            '--mouse-x',
            '50%'
          )

          card.style.setProperty(
            '--mouse-y',
            '50%'
          )

        }
      )

    })


  /* -------------------------------------------------------
     SECTION ACTIVE
  ------------------------------------------------------- */

  const sectionIds =
    nav.map(
      n => n[1].slice(1)
    )


  const updateActiveSection = () => {

    const marker =
      window.scrollY + 150

    let current = 'home'


    sectionIds.forEach((id) => {

      const element =
        document.getElementById(id)

      if (
        element &&
        element.offsetTop <= marker
      ) {
        current = id
      }

    })


    activeSection.value =
      current

  }


  $(window).on(
    'scroll',
    updateActiveSection
  )


  updateActiveSection()

})
</script>


<style>

/* =========================================================
   BASE
========================================================= */

html {
  scroll-behavior: smooth;
}

body {
  margin: 0;
}


/* =========================================================
   GRID / HERO
========================================================= */

.grid-glow {
  position: relative;
  overflow: hidden;
}

.grid-glow::before {
  content: "";
  position: absolute;
  inset: 0;

  background-image:
    linear-gradient(
      rgba(148, 163, 184, 0.08) 1px,
      transparent 1px
    ),
    linear-gradient(
      90deg,
      rgba(148, 163, 184, 0.08) 1px,
      transparent 1px
    );

  background-size: 42px 42px;

  mask-image: linear-gradient(
    to bottom,
    black,
    transparent 80%
  );

  pointer-events: none;
}

.grid-glow::after {
  content: "";
  position: absolute;

  width: 600px;
  height: 600px;

  top: -250px;
  right: -180px;

  border-radius: 9999px;

  background:
    radial-gradient(
      circle,
      rgba(239, 68, 68, 0.12),
      transparent 70%
    );

  filter: blur(20px);

  pointer-events: none;
}


/* =========================================================
   NAVIGATION
========================================================= */

.nav-link {
  position: relative;
}

.nav-active-line {
  position: absolute;

  left: 0;
  right: 0;
  bottom: -2px;

  height: 2px;

  border-radius: 999px;

  background: #ef4444;

  transform-origin: left;

  animation: navLine 0.35s ease forwards;
}

@keyframes navLine {

  from {
    transform: scaleX(0);
  }

  to {
    transform: scaleX(1);
  }

}


.nav-active-line-mobile {
  position: absolute;

  left: 12px;
  bottom: 7px;

  width: 28px;
  height: 2px;

  border-radius: 999px;

  background: #ef4444;
}


/* =========================================================
   MOBILE MENU
========================================================= */

.mobile-menu {
  animation: mobileMenu 0.3s ease forwards;
}

@keyframes mobileMenu {

  from {
    opacity: 0;
    transform: translateY(-10px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }

}


/* =========================================================
   REVEAL AU SCROLL
========================================================= */

.reveal {
  opacity: 0;

  transform:
    translateY(45px)
    scale(0.97);

  transition:
    opacity 0.8s cubic-bezier(0.22, 1, 0.36, 1),
    transform 0.8s cubic-bezier(0.22, 1, 0.36, 1);

  transition-delay:
    var(--reveal-delay, 0ms);
}


.reveal.is-visible {
  opacity: 1;

  transform:
    translateY(0)
    scale(1);
}


/* =========================================================
   PREMIUM CARD
========================================================= */

.premium-card {

  position: relative;

  overflow: hidden;

  isolation: isolate;

  --mouse-x: 50%;
  --mouse-y: 50%;

  transition:
    transform 0.5s cubic-bezier(0.22, 1, 0.36, 1),
    box-shadow 0.5s cubic-bezier(0.22, 1, 0.36, 1),
    border-color 0.4s ease;

  will-change: transform;
}


/* ---------------------------------------------------------
   Lumière dynamique
--------------------------------------------------------- */

.premium-card::before {

  content: "";

  position: absolute;

  inset: 0;

  background:
    radial-gradient(
      280px circle at var(--mouse-x) var(--mouse-y),
      rgba(239, 68, 68, 0.18),
      transparent 65%
    );

  opacity: 0;

  transition:
    opacity 0.4s ease;

  pointer-events: none;

  z-index: 0;
}


/* ---------------------------------------------------------
   Reflet
--------------------------------------------------------- */

.premium-card::after {

  content: "";

  position: absolute;

  top: -150%;
  left: -80%;

  width: 55%;
  height: 400%;

  background:
    linear-gradient(
      90deg,
      transparent,
      rgba(255, 255, 255, 0.18),
      transparent
    );

  transform:
    translateX(-120%)
    rotate(12deg);

  opacity: 0;

  pointer-events: none;

  z-index: 3;
}


/* =========================================================
   HOVER DESKTOP
========================================================= */

@media (hover: hover) and (pointer: fine) {

  .premium-card:hover {

    transform:
      translateY(-10px)
      scale(1.015);

    box-shadow:
      0 25px 60px
      rgba(15, 23, 42, 0.16);

    border-color:
      rgba(239, 68, 68, 0.35);
  }


  .premium-card:hover::before {
    opacity: 1;
  }


  .premium-card:hover::after {

    opacity: 1;

    animation:
      premiumShine
      0.9s
      ease
      forwards;
  }


  .premium-card:hover h3 {

    transform:
      translateX(3px);
  }

}


@keyframes premiumShine {

  0% {
    transform:
      translateX(-120%)
      rotate(12deg);
  }

  100% {
    transform:
      translateX(420%)
      rotate(12deg);
  }

}


/* =========================================================
   TITRES DES CARTES
========================================================= */

.premium-card h3 {

  transition:
    transform 0.35s
    cubic-bezier(0.22, 1, 0.36, 1);
}


/* =========================================================
   PROFILE IMAGE
========================================================= */

.profile-image-wrapper {

  position: relative;

  background:
    linear-gradient(
      135deg,
      #ef4444,
      #0f172a,
      #312e81
    );
}


.profile-image-wrapper::after {

  content: "";

  position: absolute;

  inset: 0;

  background:
    linear-gradient(
      120deg,
      transparent 30%,
      rgba(255,255,255,0.16),
      transparent 70%
    );

  transform:
    translateX(-120%);

  transition:
    transform 0.8s ease;

  pointer-events: none;
}


@media (hover: hover) and (pointer: fine) {

  .premium-card:hover
  .profile-image-wrapper::after {

    transform:
      translateX(120%);
  }

}


/* =========================================================
   PROJETS
========================================================= */

.project-visual {

  transition:
    transform 0.65s
    cubic-bezier(0.22, 1, 0.36, 1);
}


@media (hover: hover) and (pointer: fine) {

  .premium-card:hover
  .project-visual {

    transform:
      scale(1.035);
  }

}


/* =========================================================
   BOUTONS PREMIUM
========================================================= */

.premium-button {

  position: relative;

  overflow: hidden;

  transition:
    transform 0.35s ease,
    box-shadow 0.35s ease;
}


.premium-button::before {

  content: "";

  position: absolute;

  top: 0;
  left: -120%;

  width: 80%;
  height: 100%;

  background:
    linear-gradient(
      90deg,
      transparent,
      rgba(255,255,255,0.25),
      transparent
    );

  transform: skewX(-20deg);

  transition:
    left 0.6s ease;
}


.premium-button:hover::before {
  left: 140%;
}


.premium-button:hover {

  transform:
    translateY(-3px);

  box-shadow:
    0 15px 35px
    rgba(239, 68, 68, 0.22);
}


/* =========================================================
   SOCIAL CARDS
========================================================= */

.social-card {

  transition:
    transform 0.4s
    cubic-bezier(0.22, 1, 0.36, 1),
    box-shadow 0.4s ease;
}


.social-icon {

  display: flex;

  width: 38px;
  height: 38px;

  align-items: center;
  justify-content: center;

  border-radius: 12px;

  transition:
    transform 0.4s
    cubic-bezier(0.22, 1, 0.36, 1);
}


.social-icon svg {

  width: 21px;
  height: 21px;
}


@media (hover: hover) and (pointer: fine) {

  .social-card:hover {

    transform:
      translateY(-8px)
      scale(1.03);

    box-shadow:
      0 18px 40px
      rgba(15, 23, 42, 0.14);
  }


  .social-card:hover
  .social-icon {

    transform:
      scale(1.12)
      rotate(-4deg);
  }

}


/* =========================================================
   FOOTER SOCIALS
========================================================= */

.footer-social-list {

  display: flex;

  flex-wrap: wrap;

  gap: 10px;
}


.footer-social-item {

  display: inline-flex;

  align-items: center;
  gap: 8px;

  border-radius: 12px;

  padding: 8px 10px;

  color: #64748b;

  transition:
    transform 0.3s ease,
    color 0.3s ease,
    background 0.3s ease;
}


.footer-social-logo {

  display: flex;

  width: 28px;
  height: 28px;

  align-items: center;
  justify-content: center;

  border-radius: 8px;

  background: #f1f5f9;
}


.footer-social-logo svg {

  width: 17px;
  height: 17px;
}


.footer-social-name {

  font-size: 12px;

  font-weight: 700;
}


.footer-social-item:hover {

  transform:
    translateY(-4px);

  color: #ef4444;

  background:
    rgba(239, 68, 68, 0.06);
}


.dark .footer-social-logo {

  background:
    rgba(255,255,255,0.08);
}


/* =========================================================
   FORMULAIRE
========================================================= */

input,
textarea,
select {

  transition:
    border-color 0.25s ease,
    box-shadow 0.25s ease,
    transform 0.25s ease;
}


input:focus,
textarea:focus,
select:focus {

  transform:
    translateY(-1px);
}


/* =========================================================
   MOBILE
========================================================= */

@media (max-width: 768px) {

  .reveal {

    transform:
      translateY(30px)
      scale(0.985);
  }


  .premium-card {

    transition:
      opacity 0.7s ease,
      transform 0.5s ease;
  }


  .premium-card:active {

    transform:
      scale(0.985);
  }


  .grid-glow::after {

    width: 350px;
    height: 350px;

    top: -100px;
    right: -150px;
  }

}


/* =========================================================
   ACCESSIBILITÉ
========================================================= */

@media (prefers-reduced-motion: reduce) {

  *,
  *::before,
  *::after {

    animation-duration: 0.01ms !important;

    animation-iteration-count:
      1 !important;

    transition-duration:
      0.01ms !important;

    scroll-behavior:
      auto !important;
  }


  .reveal {

    opacity: 1;

    transform: none;
  }


  .premium-card:hover {

    transform: none;
  }

}

</style>
```

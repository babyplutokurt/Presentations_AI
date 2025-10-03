<template>
  <section
    class="slide flex min-h-screen w-full items-center justify-center bg-transparent px-6 py-12 text-slate-900 sm:px-10"
    :class="{ active: isActive }"
  >
    <div
      class="grid w-full max-w-7xl gap-12 rounded-[32px] bg-white/92 p-12 text-left shadow-2xl shadow-slate-900/20 ring-1 ring-white/60 backdrop-blur-xl transition-all duration-700 sm:p-14 lg:grid-cols-[3fr_2fr]"
      :class="isActive ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
    >
      <header class="space-y-4">
        <p class="text-sm uppercase tracking-[0.5em] text-sky-500/80">
          {{ t('slide1.kicker') }}
        </p>
        <h1 class="text-5xl font-black leading-tight text-slate-900 sm:text-6xl lg:text-7xl">
          {{ t('slide1.title') }}
        </h1>
        <img :src="portrait" alt="Intern portrait" class="mt-4 h-16 w-auto" />

      </header>

      <aside class="flex flex-col gap-7">
        <div class="rounded-3xl border border-slate-200 bg-white/95 p-8 shadow-lg shadow-slate-900/10">
          <h2 class="text-3xl font-semibold text-slate-800">
            {{ t('slide1.highlights.title') }}
          </h2>
          <ul class="mt-6 space-y-6 text-xl leading-relaxed text-slate-600">
            <li v-for="item in highlights" :key="item" class="flex items-start gap-3">
              <span class="mt-2 h-3 w-3 flex-shrink-0 rounded-full bg-sky-500"></span>
              <span>{{ item }}</span>
            </li>
          </ul>
        </div>
      </aside>
    </div>
  </section>
</template>

<script setup lang="ts">
import { computed } from 'vue'

import { useDeckI18n } from '../../shared/i18n/use-deck-i18n'
import { usePresentationContext } from '../../shared/presentation/presentation-context'
import googleLogo from './google_120dp_E3E3E3_FILL0_ROND50_wght400_GRAD0_opsz48.svg'
import portrait from './unnamed.png'

defineProps({
  isActive: Boolean,
  isPreview: Boolean
})

const presentationContext = usePresentationContext()

const { t } = useDeckI18n('internship', {
  locale: computed(() => presentationContext.state.locale),
  fallbackLocale: 'en'
})

const highlightKeys = [
  'slide1.highlights.items.maxtext',
  'slide1.highlights.items.moba'
] as const

const highlights = computed(() => highlightKeys.map(key => t(key)))
</script>

<style scoped>
.slide {
  transition: transform 0.7s ease, opacity 0.7s ease;
}
</style>

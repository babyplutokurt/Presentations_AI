<script setup lang="ts">
import { computed } from 'vue'

import BackgroundManager from '../../shared/backgrounds/background-manager.vue'
import { backgroundRegistry } from '../../shared/backgrounds/registry'
import {
  createPresentationContext,
  providePresentationContext
} from '../../shared/presentation/presentation-context'
import { useDeckI18n } from '../../shared/i18n/use-deck-i18n'
import type { LocaleCode, LocaleMeta } from '../../shared/i18n/types'

import PptContainer from '@/shared/ppt-container.vue'

import Slide1Hero from './slide-1-hero.vue'
import Slide2Background from './slide-2-background.vue'
import Slide3Problem from './slide-3-problem.vue'
import Slide4Design from './slide-4-design.vue'
import Slide5Architecture from './slide-5-architecture.vue'
import Slide6OpenaiApi from './slide-6-openai-api.vue'
import Slide7Architecture from './slide-7-architecture.vue'
import Slide8ServerPipeline from './slide-8-server-pipeline.vue'
import Slide9CoreApis from './slide-9-core-apis.vue'
import Slide10Usage from './slide-10-usage.vue'
import Slide11Runbook from './slide-11-runbook.vue'
import Slide12Demo from './slide-12-demo.vue'
import Slide13Multihost from './slide-13-multihost.vue'
import Slide14Performance from './slide-14-performance.vue'
import Slide15BenchmarkUsage from './slide-15-benchmark-usage.vue'
import portraitLogo from './unnamed.png'
import deckLocale from './locales/en.json'

type LocaleConfig = Record<LocaleCode, Pick<LocaleMeta, 'label' | 'nativeLabel' | 'direction'>>

const baseLocaleConfig = deckLocale.locales as LocaleConfig

const localeOptions: LocaleMeta[] = (Object.keys(baseLocaleConfig) as LocaleCode[]).map(code => {
  const meta = baseLocaleConfig[code]
  if (!meta) {
    throw new Error(`Missing locale metadata for code "${code}" in internship locale config`)
  }
  return {
    code,
    label: meta.label,
    nativeLabel: meta.nativeLabel,
    direction: meta.direction
  }
})

const presentationContext = createPresentationContext({
  defaults: {
    backgroundId: 'soft-mesh',
    locale: 'en'
  },
  backgrounds: backgroundRegistry,
  locales: localeOptions,
  contextKey: 'internship',
  persist: true
})

providePresentationContext(presentationContext)

const { t } = useDeckI18n('internship', {
  locale: computed(() => presentationContext.state.locale),
  fallbackLocale: 'en'
})

const presentation = computed(() => ({
  title: t('presentation.title'),
  description: t('presentation.description'),
  author: t('presentation.author'),
  date: t('presentation.dateLabel')
}))

const slides = [
  Slide1Hero,
  Slide2Background,
  Slide3Problem,
  Slide4Design,
  Slide5Architecture,
  Slide6OpenaiApi,
  Slide7Architecture,
  Slide8ServerPipeline,
  Slide9CoreApis,
  Slide10Usage,
  Slide11Runbook,
  Slide12Demo,
  Slide13Multihost,
  Slide14Performance,
  Slide15BenchmarkUsage
]

const portraitSrc = portraitLogo
</script>

<template>
  <div class="relative flex h-screen w-screen overflow-hidden bg-surface text-text-primary">
    <BackgroundManager />
    <main class="relative z-10 flex h-full w-full items-center justify-center px-6 py-6 sm:px-10">
      <div class="deck-shell h-full w-full">
        <PptContainer
          :slides="slides"
          :title="presentation.title"
          :thumbnails-label="t('labels.thumbnails')"
        />
        <img
          v-if="presentationContext.state.activeIndex !== 0"
          :src="portraitSrc"
          alt="Presenter portrait"
          class="corner-portrait"
        />
      </div>
    </main>
  </div>
</template>

<style scoped>
.deck-shell :deep(.ppt-container) {
  @apply bg-transparent;
}

.deck-shell :deep(.controls) {
  @apply fixed bottom-3 left-1/2 flex -translate-x-1/2 items-center gap-3 rounded-2xl border border-white/20 bg-white/10 px-3 py-1.5 text-xs text-text-primary shadow-xl shadow-black/40 backdrop-blur-xl;
}

.deck-shell :deep(.control-btn) {
  @apply flex h-9 w-9 items-center justify-center rounded-full bg-white/90 text-slate-900 text-sm font-semibold shadow-md shadow-black/30 ring-1 ring-black/5 transition hover:bg-white focus-visible:outline focus-visible:outline-2 focus-visible:outline-cyan-300 disabled:cursor-not-allowed disabled:opacity-40;
}

.deck-shell :deep(.slide-info) {
  @apply min-w-[56px] text-center text-xs font-semibold text-slate-900;
}

.deck-shell :deep(.progress-bar) {
  @apply fixed inset-x-0 bottom-0 h-[3px] bg-slate-900/30;
}

.deck-shell :deep(.progress) {
  @apply h-full bg-gradient-to-r from-indigo-600 via-sky-500 to-emerald-400 transition-all duration-300;
}

.deck-shell :deep(.thumbnails) {
  @apply fixed right-5 top-1/2 flex max-h-[80vh] w-72 -translate-y-1/2 flex-col overflow-hidden rounded-xl bg-slate-900/90 shadow-2xl shadow-slate-900/40 backdrop-blur-xl;
}

.corner-portrait {
  @apply pointer-events-none absolute bottom-6 right-6 h-8 w-auto drop-shadow-xl;
}

.deck-shell :deep(.thumbnails-header) {
  @apply flex items-center justify-between border-b border-white/10 px-5 py-4 text-text-primary;
}

.deck-shell :deep(.thumbnails-header h3) {
  @apply m-0 text-base font-semibold text-text-primary;
}

.deck-shell :deep(.thumbnails-header button) {
  @apply flex h-6 w-6 items-center justify-center rounded-full text-base text-text-primary transition hover:bg-white/10;
}

.deck-shell :deep(.thumbnails-grid) {
  @apply max-h-[60vh] overflow-y-auto px-4 py-4;
}

.deck-shell :deep(.thumbnail) {
  @apply relative mb-3 h-28 w-full overflow-hidden rounded-lg bg-white/5 transition hover:scale-[1.02] hover:bg-white/10;
}

.deck-shell :deep(.thumbnail.active) {
  @apply border-2 border-sky-300 bg-sky-400/20;
}

.deck-shell :deep(.thumbnail-number) {
  @apply absolute left-2 top-2 rounded-md bg-slate-900/80 px-2 py-1 text-xs font-semibold text-text-primary shadow-sm shadow-black/40;
}

@media (max-width: 768px) {
  .deck-shell :deep(.thumbnails) {
    @apply right-5 w-[calc(100vw-40px)];
  }

  .deck-shell :deep(.controls) {
    @apply gap-3 px-4 py-2;
  }

  .deck-shell :deep(.control-btn) {
    @apply h-10 w-10;
  }
}
</style>

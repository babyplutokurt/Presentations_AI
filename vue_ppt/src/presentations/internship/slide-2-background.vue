<template>
  <section
    class="slide flex min-h-screen w-full items-center justify-center bg-transparent px-6 py-12 text-slate-900 sm:px-10"
    :class="{ active: isActive }"
  >
    <div
      class="w-full max-w-4xl space-y-6 rounded-[32px] bg-white/94 p-12 shadow-2xl shadow-slate-900/20 ring-1 ring-white/60 backdrop-blur-xl transition-all duration-700 sm:p-14"
      :class="isActive ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'"
    >
      <div class="space-y-6">
        <p class="text-xs font-semibold uppercase tracking-[0.5em] text-sky-600">
          {{ t('slide2.kicker') }}
        </p>
        <h2 class="text-4xl font-black tracking-tight text-slate-900 sm:text-5xl">
          {{ t('slide2.title') }}
        </h2>

        <div class="space-y-4">
          <div class="rounded-3xl border border-slate-200 bg-white/96 p-7 shadow-md shadow-slate-900/10">
            <h3 class="text-sm font-semibold uppercase tracking-[0.3em] text-slate-500">
              {{ t('slide2.project.name') }}
            </h3>
            <p class="mt-4 text-2xl font-semibold text-slate-800">
              {{ t('slide2.project.tldr.heading') }}
            </p>
            <p class="mt-4 text-base leading-relaxed text-slate-600">
              {{ t('slide2.project.tldr.body') }}
            </p>
          </div>

          <div class="rounded-3xl border border-transparent bg-gradient-to-r from-sky-500/18 to-emerald-400/18 p-[1px]">
            <div class="rounded-[calc(theme(borderRadius.3xl)-1px)] bg-white p-7">
              <h3 class="text-lg font-semibold text-slate-900">
                {{ t('slide2.objective.title') }}
              </h3>
              <p class="mt-3 text-base leading-relaxed text-slate-600">
                {{ t('slide2.objective.body') }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { computed } from 'vue'

import { useDeckI18n } from '../../shared/i18n/use-deck-i18n'
import { usePresentationContext } from '../../shared/presentation/presentation-context'

defineProps({
  isActive: Boolean,
  isPreview: Boolean
})

const presentationContext = usePresentationContext()

const { t } = useDeckI18n('internship', {
  locale: computed(() => presentationContext.state.locale),
  fallbackLocale: 'en'
})

// Requirements list intentionally removed per latest content direction.
</script>

<style scoped>
.slide {
  transition: transform 0.7s ease, opacity 0.7s ease;
}
</style>

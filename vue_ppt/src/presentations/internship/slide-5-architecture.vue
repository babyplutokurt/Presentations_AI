<template>
  <section class="slide-shell" :class="{ active: isActive }">
    <div class="panel">
      <header class="headline-group">
        <p class="eyebrow">{{ t('slide5.kicker') }}</p>
        <h2>{{ t('slide5.title') }}</h2>
      </header>

      <p class="lede">{{ t('slide5.lede') }}</p>

      <div class="view-toggle" role="tablist" aria-label="Slide view switch">
        <button
          class="toggle-pill"
          type="button"
          role="tab"
          :aria-selected="viewMode === 'comparison'"
          :class="{ active: viewMode === 'comparison' }"
          @click="setViewMode('comparison')"
        >
          {{ t('slide5.viewToggle.comparison') }}
        </button>

        <button
          class="toggle-pill"
          type="button"
          role="tab"
          :aria-selected="viewMode === 'decision'"
          :class="{ active: viewMode === 'decision' }"
          @click="setViewMode('decision')"
        >
          {{ t('slide5.viewToggle.decision') }}
        </button>
      </div>

      <div v-if="viewMode === 'comparison'" class="comparison-grid">
        <article class="option-card option-card--native">
          <header class="option-header">
            <h3>{{ t('slide5.native.title') }}</h3>
            <p class="summary">{{ t('slide5.native.summary') }}</p>
          </header>

          <div class="list-card list-card--risk">
            <h4>{{ t('slide5.native.consTitle') }}</h4>
            <ul>
              <li v-for="item in nativeCons" :key="item">
                <span class="bullet bullet-risk"></span>
                <span>{{ item }}</span>
              </li>
            </ul>
          </div>
        </article>

        <article class="option-card option-card--server">
          <header class="option-header">
            <h3>{{ t('slide5.server.title') }}</h3>
            <p class="summary">{{ t('slide5.server.summary') }}</p>
          </header>

          <div class="list-card list-card--positive">
            <h4>{{ t('slide5.server.prosTitle') }}</h4>
            <ul>
              <li v-for="item in serverPros" :key="item">
                <span class="bullet bullet-positive"></span>
                <span>{{ item }}</span>
              </li>
            </ul>
          </div>
        </article>
      </div>

      <div v-else class="decision-panel">
        <header class="decision-header">
          <p class="decision-eyebrow">{{ t('slide5.decision.label') }}</p>
          <h3>{{ t('slide5.decision.title') }}</h3>
        </header>
        <p class="decision-copy">{{ t('slide5.decision.copy') }}</p>

        <div class="impact-widget">
          <span class="impact-label">{{ t('slide5.decision.widget.label') }}</span>
          <p>{{ t('slide5.decision.widget.copy') }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'

import { useDeckI18n } from '../../shared/i18n/use-deck-i18n'
import { usePresentationContext } from '../../shared/presentation/presentation-context'

const props = defineProps({
  isActive: Boolean,
  isPreview: Boolean
})

const presentationContext = usePresentationContext()

const { t } = useDeckI18n('internship', {
  locale: computed(() => presentationContext.state.locale),
  fallbackLocale: 'en'
})

type ViewMode = 'comparison' | 'decision'

const viewMode = ref<ViewMode>('comparison')

const setViewMode = (mode: ViewMode) => {
  viewMode.value = mode
}

const nativeConsKeys = [
  'slide5.native.cons.externalDependency',
  'slide5.native.cons.runtimeVariance'
] as const

const serverProsKeys = [
  'slide5.server.pros.decoupling',
  'slide5.server.pros.standardInterface',
  'slide5.server.pros.batchAcceleration'
] as const

const nativeCons = computed(() => nativeConsKeys.map(key => t(key)))
const serverPros = computed(() => serverProsKeys.map(key => t(key)))
</script>

<style scoped>
.slide-shell {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  width: 100%;
  padding: clamp(2.5rem, 7vw, 5.5rem);
  transition: transform 0.7s ease, opacity 0.7s ease;
}

.slide-shell:not(.active) {
  transform: translateY(12px);
  opacity: 0;
}

.panel {
  width: min(100%, 1180px);
  display: flex;
  flex-direction: column;
  gap: clamp(1.6rem, 3.6vw, 2.4rem);
  padding: clamp(1.9rem, 4vw, 3.1rem);
  border-radius: clamp(32px, 6vw, 48px);
  background:
    radial-gradient(circle at 12% 18%, rgba(52, 168, 83, 0.16), transparent 58%),
    radial-gradient(circle at 88% 82%, rgba(66, 133, 244, 0.18), transparent 60%),
    linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(243, 249, 255, 0.96));
  box-shadow: 0 45px 90px rgba(15, 23, 42, 0.14);
  backdrop-filter: blur(18px);
}

.headline-group {
  text-align: center;
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
}

.headline-group h2 {
  margin: 0;
  font-size: clamp(2.2rem, 4.4vw, 3rem);
  font-weight: 800;
  letter-spacing: -0.02em;
  color: #0f172a;
}

.eyebrow {
  margin: 0;
  font-size: 0.78rem;
  font-weight: 600;
  letter-spacing: 0.55em;
  text-transform: uppercase;
  color: rgba(234, 67, 53, 0.7);
}

.lede {
  margin: 0 auto;
  max-width: 760px;
  text-align: center;
  font-size: clamp(1.05rem, 2.1vw, 1.3rem);
  line-height: 1.65;
  color: rgba(15, 23, 42, 0.8);
}

.view-toggle {
  display: inline-flex;
  align-self: center;
  border-radius: 999px;
  padding: 0.35rem;
  background: rgba(148, 163, 184, 0.15);
  gap: 0.35rem;
}

.toggle-pill {
  min-width: 160px;
  border: none;
  border-radius: 999px;
  padding: 0.55rem 1.4rem;
  font-size: 0.92rem;
  font-weight: 600;
  color: rgba(15, 23, 42, 0.65);
  background: transparent;
  cursor: pointer;
  transition: background 200ms ease, color 200ms ease, box-shadow 200ms ease;
}

.toggle-pill:hover {
  background: rgba(255, 255, 255, 0.6);
  color: rgba(15, 23, 42, 0.82);
}

.toggle-pill.active {
  background: linear-gradient(135deg, rgba(66, 133, 244, 0.28), rgba(52, 168, 83, 0.28));
  color: #0f172a;
  box-shadow: 0 10px 24px rgba(15, 23, 42, 0.18);
}

.comparison-grid {
  display: grid;
  gap: clamp(1.4rem, 3vw, 2rem);
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
}

.option-card {
  display: flex;
  flex-direction: column;
  gap: 1.2rem;
  padding: clamp(1.6rem, 3.2vw, 2.2rem);
  border-radius: 28px;
  border: 1px solid rgba(148, 163, 184, 0.2);
  background: rgba(255, 255, 255, 0.9);
  box-shadow: 0 28px 62px rgba(15, 23, 42, 0.12);
}

.option-card--native {
  border-color: rgba(234, 67, 53, 0.2);
}

.option-card--server {
  border-color: rgba(66, 133, 244, 0.24);
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.94), rgba(219, 234, 254, 0.9));
}

.option-header {
  display: flex;
  flex-direction: column;
  gap: 0.7rem;
}

.option-header h3 {
  margin: 0;
  font-size: clamp(1.5rem, 3vw, 1.9rem);
  font-weight: 700;
  color: #0f172a;
}

.summary {
  margin: 0;
  font-size: 1rem;
  line-height: 1.6;
  color: rgba(15, 23, 42, 0.72);
}

.list-card {
  border-radius: 20px;
  padding: 1.2rem 1.4rem;
  background: rgba(255, 255, 255, 0.92);
  border: 1px solid rgba(148, 163, 184, 0.18);
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.list-card--positive {
  border-color: rgba(52, 168, 83, 0.3);
}

.list-card--risk {
  border-color: rgba(234, 67, 53, 0.28);
}

.list-card h4 {
  margin: 0;
  font-size: 0.98rem;
  font-weight: 700;
  color: rgba(15, 23, 42, 0.85);
}

.list-card ul {
  margin: 0;
  padding: 0;
  list-style: none;
  display: grid;
  gap: 0.7rem;
}

.list-card li {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 0.65rem;
  align-items: start;
  font-size: 0.98rem;
  line-height: 1.55;
  color: rgba(15, 23, 42, 0.78);
}

.bullet {
  display: inline-flex;
  height: 10px;
  width: 10px;
  margin-top: 0.45rem;
  border-radius: 50%;
}

.bullet-positive {
  background: linear-gradient(135deg, #34a853, #0f9d58);
}

.bullet-risk {
  background: linear-gradient(135deg, #ea4335, #c5221f);
}

.decision-panel {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  align-items: center;
  text-align: center;
  padding: clamp(1.8rem, 3.4vw, 2.6rem);
  border-radius: 28px;
  background: linear-gradient(135deg, rgba(66, 133, 244, 0.18), rgba(52, 168, 83, 0.18));
  border: 1px solid rgba(66, 133, 244, 0.38);
  box-shadow: 0 28px 62px rgba(15, 23, 42, 0.12);
}

.decision-header {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
  align-items: center;
}

.decision-eyebrow {
  margin: 0;
  font-size: 0.78rem;
  font-weight: 700;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  color: rgba(15, 23, 42, 0.75);
}

.decision-header h3 {
  margin: 0;
  font-size: clamp(1.6rem, 3.2vw, 2.1rem);
  font-weight: 700;
  color: #0f172a;
}

.decision-copy {
  margin: 0;
  font-size: 1.08rem;
  line-height: 1.7;
  color: rgba(15, 23, 42, 0.85);
  max-width: 640px;
}

.impact-widget {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
  margin-top: 1.4rem;
  padding: 1rem 1.3rem;
  border-radius: 16px;
  background: rgba(15, 23, 42, 0.08);
  border: 1px solid rgba(148, 163, 184, 0.28);
  max-width: 520px;
}

.impact-label {
  font-size: 0.78rem;
  font-weight: 700;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: rgba(15, 23, 42, 0.72);
}

.impact-widget p {
  margin: 0;
  font-size: 0.98rem;
  line-height: 1.6;
  color: rgba(15, 23, 42, 0.78);
}

@media (max-width: 960px) {
  .comparison-grid {
    grid-template-columns: 1fr;
  }
}
</style>

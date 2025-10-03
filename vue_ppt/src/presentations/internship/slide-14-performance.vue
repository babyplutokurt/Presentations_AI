<template>
  <section class="slide-shell" :class="{ active: isActive }">
    <div class="panel">
      <header class="headline-group">
        <p class="eyebrow">{{ t('slide14.kicker') }}</p>
        <h2>{{ t('slide14.title') }}</h2>
      </header>

      <p class="lede">{{ t('slide14.lede') }}</p>

      <div class="chart-grid">
        <article v-for="benchmark in benchmarks" :key="benchmark.id" class="chart-card">
          <header class="chart-header">
            <div>
              <p class="badge">{{ benchmark.hardware }}</p>
              <h3>{{ benchmark.title }}</h3>
            </div>
            <span class="model">{{ benchmark.model }}</span>
          </header>

          <div class="bars">
            <div class="bar-row">
              <span class="bar-label">{{ t('slide14.labels.existing') }}</span>
              <div class="bar-track">
                <span class="bar bar--existing" :style="{ width: benchmark.existingWidth }"></span>
              </div>
              <span class="bar-value">{{ benchmark.existingLabel }}</span>
            </div>

            <div class="bar-row">
              <span class="bar-label">{{ t('slide14.labels.newDesign') }}</span>
              <div class="bar-track">
                <span class="bar bar--new" :style="{ width: benchmark.newWidth }"></span>
              </div>
              <span class="bar-value">{{ benchmark.newLabel }}</span>
            </div>
          </div>

          <footer class="delta">
            <span class="delta-label">{{ t('slide14.labels.speedup') }}</span>
            <span class="delta-value">×{{ benchmark.speedup }}</span>
          </footer>
        </article>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { computed } from 'vue'

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

const benchmarks = computed(() => {
  const cases = [
    {
      id: 'v5p8-0shot',
      hardware: t('slide14.v5p8_0shot.hardware'),
      title: t('slide14.v5p8_0shot.title'),
      model: t('slide14.v5p8_0shot.model'),
      existingHours: 13,
      newHours: 1,
      existingLabel: t('slide14.v5p8_0shot.existingLabel'),
      newLabel: t('slide14.v5p8_0shot.newLabel')
    },
    {
      id: 'v5p8-5shot',
      hardware: t('slide14.v5p8_5shot.hardware'),
      title: t('slide14.v5p8_5shot.title'),
      model: t('slide14.v5p8_5shot.model'),
      existingHours: 55,
      newHours: 1.3,
      existingLabel: t('slide14.v5p8_5shot.existingLabel'),
      newLabel: t('slide14.v5p8_5shot.newLabel')
    },
    {
      id: 'v5p64',
      hardware: t('slide14.v5p64.hardware'),
      title: t('slide14.v5p64.title'),
      model: t('slide14.v5p64.model'),
      existingHours: 83,
      newHours: 11,
      existingLabel: t('slide14.v5p64.existingLabel'),
      newLabel: t('slide14.v5p64.newLabel')
    }
  ] as const

  return cases.map(entry => {
    const max = Math.max(entry.existingHours, entry.newHours)
    const existingWidth = `${(entry.existingHours / max) * 100}%`
    const newWidth = `${(entry.newHours / max) * 100}%`
    const speedup = (entry.existingHours / entry.newHours).toFixed(1)

    return {
      ...entry,
      existingWidth,
      newWidth,
      speedup
    }
  })
})
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
  width: min(100%, 1340px);
  display: flex;
  flex-direction: column;
  gap: clamp(1.6rem, 3.4vw, 2.3rem);
  padding: clamp(1.9rem, 4vw, 3.1rem);
  border-radius: clamp(32px, 6vw, 48px);
  background:
    radial-gradient(circle at 12% 16%, rgba(66, 133, 244, 0.18), transparent 58%),
    radial-gradient(circle at 88% 84%, rgba(52, 168, 83, 0.16), transparent 60%),
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
  color: rgba(52, 168, 83, 0.7);
}

.lede {
  margin: 0 auto;
  max-width: 860px;
  text-align: center;
  font-size: clamp(1.05rem, 2.1vw, 1.28rem);
  line-height: 1.65;
  color: rgba(15, 23, 42, 0.8);
}

.chart-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(340px, 1fr));
  gap: clamp(1.4rem, 3vw, 2.4rem);
}

.chart-card {
  display: flex;
  flex-direction: column;
  gap: 1.1rem;
  padding: clamp(1.6rem, 3.2vw, 2.4rem);
  border-radius: 30px;
  border: 1px solid rgba(148, 163, 184, 0.2);
  background: rgba(255, 255, 255, 0.94);
  box-shadow: 0 22px 52px rgba(15, 23, 42, 0.1);
}

.chart-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 1rem;
}

.badge {
  margin: 0;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.28em;
  text-transform: uppercase;
  color: rgba(15, 23, 42, 0.65);
}

.chart-header h3 {
  margin: 0.2rem 0 0;
  font-size: clamp(1.3rem, 2.6vw, 1.7rem);
  font-weight: 700;
  color: #0f172a;
}

.model {
  font-size: 0.9rem;
  font-weight: 600;
  color: rgba(15, 23, 42, 0.65);
}

.bars {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.bar-row {
  display: grid;
  grid-template-columns: 120px 1fr auto;
  align-items: center;
  gap: 0.8rem;
}

.bar-label {
  font-size: 0.9rem;
  font-weight: 600;
  color: rgba(15, 23, 42, 0.7);
  text-transform: uppercase;
  letter-spacing: 0.12em;
}

.bar-track {
  position: relative;
  height: 14px;
  border-radius: 999px;
  background: rgba(148, 163, 184, 0.2);
  overflow: hidden;
}

.bar {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  border-radius: 999px;
}

.bar--existing {
  background: linear-gradient(90deg, rgba(148, 163, 184, 0.75), rgba(71, 85, 105, 0.9));
}

.bar--new {
  background: linear-gradient(90deg, rgba(52, 211, 153, 0.85), rgba(14, 165, 233, 0.9));
}

.bar-value {
  font-size: 0.95rem;
  font-weight: 600;
  color: rgba(15, 23, 42, 0.85);
}

.delta {
  display: flex;
  justify-content: flex-end;
  align-items: baseline;
  gap: 0.6rem;
}

.delta-label {
  font-size: 0.8rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.14em;
  color: rgba(15, 23, 42, 0.6);
}

.delta-value {
  font-size: 1.4rem;
  font-weight: 800;
  color: #047857;
}

@media (max-width: 1024px) {
  .bar-row {
    grid-template-columns: 100px 1fr auto;
  }

  .chart-grid {
    grid-template-columns: 1fr;
  }
}
</style>

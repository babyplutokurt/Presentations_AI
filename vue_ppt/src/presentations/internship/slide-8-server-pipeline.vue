<template>
  <section class="slide-shell" :class="{ active: isActive }">
    <div class="panel">
      <header class="headline-group">
        <p class="eyebrow">{{ t('slide8.kicker') }}</p>
        <h2>{{ t('slide8.title') }}</h2>
      </header>

      <p class="lede">{{ t('slide8.lede') }}</p>

      <div class="pipeline">
        <article class="stage stage--ingest">
          <header class="stage-header">
            <span class="badge">{{ t('slide8.ingest.badge') }}</span>
            <h3>{{ t('slide8.ingest.title') }}</h3>
          </header>
          <p class="stage-body">{{ t('slide8.ingest.summary') }}</p>
        </article>

        <article class="stage stage--batching">
          <header class="stage-header">
            <span class="badge badge--accent">{{ t('slide8.batch.badge') }}</span>
            <h3>{{ t('slide8.batch.title') }}</h3>
          </header>
          <p class="stage-body">{{ t('slide8.batch.summary') }}</p>
        </article>

        <article class="stage stage--dispatch">
          <header class="stage-header">
            <span class="badge badge--emerald">{{ t('slide8.dispatch.badge') }}</span>
            <h3>{{ t('slide8.dispatch.title') }}</h3>
          </header>
          <p class="stage-body">{{ t('slide8.dispatch.summary') }}</p>
        </article>
      </div>

      <footer class="footnote">
        <span class="footnote-label">{{ t('slide8.labels.result') }}</span>
        <p>{{ t('slide8.footnote') }}</p>
      </footer>
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

// Stage descriptions are provided directly via localized summaries.
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
    radial-gradient(circle at 88% 84%, rgba(251, 188, 5, 0.16), transparent 60%),
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
  max-width: 860px;
  text-align: center;
  font-size: clamp(1.05rem, 2.1vw, 1.28rem);
  line-height: 1.65;
  color: rgba(15, 23, 42, 0.8);
}

.pipeline {
  display: grid;
  grid-template-columns: repeat(3, minmax(240px, 1fr));
  gap: clamp(1.4rem, 3vw, 2.2rem);
}

.connector {
  display: none;
}

.stage {
  display: flex;
  flex-direction: column;
  gap: 1.2rem;
  padding: clamp(1.6rem, 3.2vw, 2.4rem);
  border-radius: 30px;
  border: 1px solid rgba(148, 163, 184, 0.2);
  background: rgba(255, 255, 255, 0.94);
  box-shadow: 0 22px 52px rgba(15, 23, 42, 0.1);
}

.stage--batching {
  border-color: rgba(251, 188, 5, 0.3);
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(253, 246, 178, 0.92));
}

.stage--dispatch {
  border-color: rgba(52, 168, 83, 0.28);
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(224, 247, 250, 0.9));
}

.stage-header {
  display: flex;
  flex-direction: column;
  gap: 0.65rem;
}

.stage-header h3 {
  margin: 0;
  font-size: clamp(1.45rem, 2.8vw, 1.9rem);
  font-weight: 700;
  color: #0f172a;
}

.stage-header p {
  margin: 0;
  font-size: 1rem;
  line-height: 1.6;
  color: rgba(15, 23, 42, 0.72);
}

.connector,
.chevron,
.chevron::after {
  display: none;
}

.stage-body {
  margin: 0;
  font-size: 0.98rem;
  line-height: 1.6;
  color: rgba(15, 23, 42, 0.78);
}

.badge {
  align-self: flex-start;
  padding: 0.3rem 0.8rem;
  border-radius: 999px;
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  background: rgba(66, 133, 244, 0.16);
  color: rgba(15, 23, 42, 0.72);
}

.badge--accent {
  background: rgba(251, 188, 5, 0.22);
}

.badge--emerald {
  background: rgba(52, 168, 83, 0.2);
}

.footnote {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
  padding: 1rem 1.2rem;
  border-radius: 18px;
  background: rgba(59, 130, 246, 0.08);
  border: 1px solid rgba(59, 130, 246, 0.22);
}

.footnote-label {
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: rgba(15, 23, 42, 0.7);
}

.footnote p {
  margin: 0;
  font-size: 0.95rem;
  line-height: 1.6;
  color: rgba(15, 23, 42, 0.78);
}

@media (max-width: 1024px) {
  .pipeline {
    grid-template-columns: 1fr;
  }
}
</style>

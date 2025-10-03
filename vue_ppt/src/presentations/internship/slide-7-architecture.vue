<template>
  <section class="slide-shell" :class="{ active: isActive }">
    <div class="panel">
      <header class="headline-group">
        <p class="eyebrow">{{ t('slide7.kicker') }}</p>
        <h2>{{ t('slide7.title') }}</h2>
      </header>

      <p class="lede">{{ t('slide7.lede') }}</p>

      <div class="diagram">
        <div class="lane lane--client">
          <header class="lane-header">
            <span class="badge">{{ t('slide7.client.badge') }}</span>
            <h3>{{ t('slide7.client.title') }}</h3>
            <p>{{ t('slide7.client.summary') }}</p>
          </header>
        </div>

        <div class="lane lane--api">
          <header class="lane-header">
            <span class="badge badge--accent">{{ t('slide7.api.badge') }}</span>
            <h3>{{ t('slide7.api.title') }}</h3>
            <p>{{ t('slide7.api.summary') }}</p>
          </header>
        </div>

        <div class="lane lane--backend">
          <header class="lane-header">
            <span class="badge badge--emerald">{{ t('slide7.backend.badge') }}</span>
            <h3>{{ t('slide7.backend.title') }}</h3>
            <p>{{ t('slide7.backend.summary') }}</p>
          </header>
        </div>
      </div>

      <footer class="footnote">
        <span class="footnote-label">{{ t('slide7.labels.framing') }}</span>
        <p>{{ t('slide7.footnote') }}</p>
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
  width: min(100%, 1280px);
  display: flex;
  flex-direction: column;
  gap: clamp(1.6rem, 3.4vw, 2.3rem);
  padding: clamp(1.9rem, 4vw, 3.1rem);
  border-radius: clamp(32px, 6vw, 48px);
  background:
    radial-gradient(circle at 14% 16%, rgba(66, 133, 244, 0.18), transparent 58%),
    radial-gradient(circle at 86% 86%, rgba(15, 157, 88, 0.16), transparent 60%),
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
  color: rgba(251, 188, 5, 0.7);
}

.lede {
  margin: 0 auto;
  max-width: 820px;
  text-align: center;
  font-size: clamp(1.05rem, 2.1vw, 1.28rem);
  line-height: 1.65;
  color: rgba(15, 23, 42, 0.8);
}

.diagram {
  display: grid;
  grid-template-columns: repeat(3, minmax(280px, 1fr));
  align-items: stretch;
  gap: clamp(1.4rem, 3vw, 2rem);
}

.lane {
  display: flex;
  flex-direction: column;
  gap: 1.1rem;
  padding: clamp(1.6rem, 3.2vw, 2.4rem);
  border-radius: 28px;
  border: 1px solid rgba(148, 163, 184, 0.2);
  background: rgba(255, 255, 255, 0.94);
  box-shadow: 0 22px 52px rgba(15, 23, 42, 0.1);
}

.lane--client {
  border-color: rgba(66, 133, 244, 0.28);
}

.lane--api {
  border-color: rgba(251, 188, 5, 0.32);
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(253, 246, 178, 0.92));
}

.lane--backend {
  border-color: rgba(15, 157, 88, 0.3);
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(220, 252, 231, 0.92));
}

.lane-header {
  display: flex;
  flex-direction: column;
  gap: 0.65rem;
}

.lane-header h3 {
  margin: 0;
  font-size: clamp(1.45rem, 2.8vw, 1.9rem);
  font-weight: 700;
  color: #0f172a;
}

.lane-header p {
  margin: 0;
  font-size: 1rem;
  line-height: 1.6;
  color: rgba(15, 23, 42, 0.72);
}

.badge {
  align-self: flex-start;
  padding: 0.28rem 0.75rem;
  border-radius: 999px;
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  background: rgba(66, 133, 244, 0.14);
  color: rgba(15, 23, 42, 0.7);
}

.badge--accent {
  background: rgba(251, 188, 5, 0.22);
}

.badge--emerald {
  background: rgba(15, 157, 88, 0.2);
}

.feature-grid {
  display: grid;
  gap: clamp(1rem, 2vw, 1.4rem);
}

.feature-card {
  border-radius: 18px;
  border: 1px solid rgba(148, 163, 184, 0.2);
  background: rgba(255, 255, 255, 0.9);
  padding: 1rem 1.2rem;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.feature-card h4 {
  margin: 0;
  font-size: 1rem;
  font-weight: 700;
  color: rgba(15, 23, 42, 0.85);
}

.feature-card p {
  margin: 0;
  font-size: 0.95rem;
  line-height: 1.55;
  color: rgba(15, 23, 42, 0.8);
}

.bullet-list {
  margin: 0;
  padding: 0;
  list-style: none;
  display: grid;
  gap: 0.7rem;
}

.bullet-list li {
  display: grid;
  grid-template-columns: 18px 1fr;
  align-items: start;
  gap: 0.7rem;
  font-size: 0.98rem;
  line-height: 1.55;
  color: rgba(15, 23, 42, 0.78);
}

.icon {
  margin-top: 0.3rem;
  height: 12px;
  width: 12px;
  border-radius: 50%;
  background: linear-gradient(135deg, rgba(66, 133, 244, 0.9), rgba(15, 157, 88, 0.9));
  box-shadow: 0 0 0 4px rgba(66, 133, 244, 0.12);
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
  .diagram {
    grid-template-columns: 1fr;
  }
}
</style>

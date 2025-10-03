<template>
  <section class="slide-shell" :class="{ active: isActive }">
    <div class="panel">
      <header class="headline-group">
        <p class="eyebrow">{{ t('slide13.kicker') }}</p>
        <h2>{{ t('slide13.title') }}</h2>
      </header>

      <p class="lede">{{ t('slide13.lede') }}</p>

      <div class="content">
        <figure class="diagram">
          <img :src="topology" :alt="t('slide13.labels.diagramAlt')" />
          <figcaption>{{ t('slide13.labels.diagramCaption') }}</figcaption>
        </figure>

        <div class="notes">
          <section>
            <h3>{{ t('slide13.points.host0.title') }}</h3>
            <p>{{ t('slide13.points.host0.body') }}</p>
          </section>

          <section>
            <h3>{{ t('slide13.points.portforward.title') }}</h3>
            <p>{{ t('slide13.points.portforward.body') }}</p>
            <pre class="code-block" aria-label="Port forward command"><code>{{ t('slide13.points.portforward.command') }}</code></pre>
          </section>

          <section>
            <h3>{{ t('slide13.points.broadcast.title') }}</h3>
            <p>{{ t('slide13.points.broadcast.body') }}</p>
          </section>
        </div>
      </div>

      <footer class="footnote">
        <span class="footnote-label">{{ t('slide13.labels.tip') }}</span>
        <p>{{ t('slide13.footnote') }}</p>
      </footer>
    </div>
  </section>
</template>

<script setup lang="ts">
import { computed } from 'vue'

import topology from './multi-pods.png'
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

.content {
  display: grid;
  grid-template-columns: minmax(360px, 1.1fr) minmax(320px, 1fr);
  gap: clamp(1.4rem, 3vw, 2.4rem);
  align-items: center;
}

.diagram {
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
  align-items: center;
  padding: clamp(1.4rem, 3vw, 2.1rem);
  border-radius: 28px;
  background: rgba(255, 255, 255, 0.94);
  border: 1px solid rgba(148, 163, 184, 0.2);
  box-shadow: 0 22px 52px rgba(15, 23, 42, 0.1);
}

.diagram img {
  width: min(100%, 520px);
  border-radius: 18px;
}

.diagram figcaption {
  margin: 0;
  font-size: 0.85rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: rgba(71, 85, 105, 0.8);
}

.notes {
  display: grid;
  gap: clamp(1rem, 2vw, 1.6rem);
}

.notes section {
  display: flex;
  flex-direction: column;
  gap: 0.45rem;
}

.notes h3 {
  margin: 0;
  font-size: 1.05rem;
  font-weight: 700;
  color: #0f172a;
}

.notes p {
  margin: 0;
  font-size: 0.98rem;
  line-height: 1.6;
  color: rgba(15, 23, 42, 0.78);
}

.code-block {
  margin: 0;
  padding: 0.9rem 1.1rem;
  border-radius: 16px;
  background: #0f172a;
  color: #e2e8f0;
  font-family: 'Fira Code', 'SFMono-Regular', Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace;
  font-size: 0.9rem;
  line-height: 1.6;
  white-space: pre-wrap;
  border: 1px solid rgba(148, 163, 184, 0.32);
}

.bullet-list {
  margin: 0;
  padding: 0;
  list-style: none;
}

.icon {
  display: none;
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
  .content {
    grid-template-columns: 1fr;
  }

  .diagram img {
    width: 100%;
  }
}
</style>

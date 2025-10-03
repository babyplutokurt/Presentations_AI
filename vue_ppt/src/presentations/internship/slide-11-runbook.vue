<template>
  <section class="slide-shell" :class="{ active: isActive }">
    <div class="panel">
      <header class="headline-group">
        <p class="eyebrow">{{ t('slide11.kicker') }}</p>
        <h2>{{ t('slide11.title') }}</h2>
      </header>

      <p class="lede">{{ t('slide11.lede') }}</p>

      <div class="runbook">
        <article class="step-card">
          <header class="step-header">
            <span class="step-number">1</span>
            <div>
              <h3>{{ t('slide11.step1.title') }}</h3>
              <p>{{ t('slide11.step1.summary') }}</p>
            </div>
          </header>

          <pre class="code-block" aria-label="Server startup command"><code>{{ t('slide11.step1.command') }}</code></pre>

          <ul class="bullet-list">
            <li v-for="item in step1Bullets" :key="item">
              <span class="icon"></span>
              <span>{{ item }}</span>
            </li>
          </ul>
        </article>

        <article class="step-card">
          <header class="step-header">
            <span class="step-number">2</span>
            <div>
              <h3>{{ t('slide11.step2.title') }}</h3>
              <p>{{ t('slide11.step2.summary') }}</p>
            </div>
          </header>

          <pre class="code-block" aria-label="Evaluation command"><code>{{ t('slide11.step2.command') }}</code></pre>

          <ul class="bullet-list">
            <li v-for="item in step2Bullets" :key="item">
              <span class="icon"></span>
              <span>{{ item }}</span>
            </li>
          </ul>
        </article>
      </div>

      <footer class="footnote">
        <span class="footnote-label">{{ t('slide11.labels.tip') }}</span>
        <p>{{ t('slide11.footnote') }}</p>
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

const step1Keys = [
  'slide11.step1.points.modelConfig',
  'slide11.step1.points.batchTpu'
] as const

const step2Keys = [
  'slide11.step2.points.leverageLocal',
  'slide11.step2.points.fastIter'
] as const

const step1Bullets = computed(() => step1Keys.map(key => t(key)))
const step2Bullets = computed(() => step2Keys.map(key => t(key)))
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
  width: min(100%, 1260px);
  display: flex;
  flex-direction: column;
  gap: clamp(1.6rem, 3.4vw, 2.3rem);
  padding: clamp(1.9rem, 4vw, 3.1rem);
  border-radius: clamp(32px, 6vw, 48px);
  background:
    radial-gradient(circle at 12% 16%, rgba(66, 133, 244, 0.18), transparent 58%),
    radial-gradient(circle at 88% 84%, rgba(15, 157, 88, 0.16), transparent 60%),
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
  color: rgba(59, 130, 246, 0.7);
}

.lede {
  margin: 0 auto;
  max-width: 820px;
  text-align: center;
  font-size: clamp(1.05rem, 2.1vw, 1.28rem);
  line-height: 1.65;
  color: rgba(15, 23, 42, 0.8);
}

.runbook {
  display: grid;
  gap: clamp(1.4rem, 3vw, 2.2rem);
  grid-template-columns: repeat(auto-fit, minmax(480px, 1fr));
}

.step-card {
  display: flex;
  flex-direction: column;
  gap: 1.2rem;
  padding: clamp(1.6rem, 3.2vw, 2.4rem);
  border-radius: 30px;
  border: 1px solid rgba(148, 163, 184, 0.2);
  background: rgba(255, 255, 255, 0.94);
  box-shadow: 0 22px 52px rgba(15, 23, 42, 0.1);
}

.step-header {
  display: flex;
  gap: 1rem;
  align-items: flex-start;
}

.step-number {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  height: 40px;
  width: 40px;
  border-radius: 50%;
  font-size: 1.1rem;
  font-weight: 700;
  background: linear-gradient(135deg, rgba(59, 130, 246, 0.24), rgba(52, 168, 83, 0.24));
  color: #0f172a;
  box-shadow: 0 12px 28px rgba(15, 23, 42, 0.12);
}

.step-header h3 {
  margin: 0;
  font-size: clamp(1.45rem, 2.8vw, 1.9rem);
  font-weight: 700;
  color: #0f172a;
}

.step-header p {
  margin: 0.3rem 0 0;
  font-size: 1rem;
  line-height: 1.6;
  color: rgba(15, 23, 42, 0.72);
}

.code-block {
  margin: 0;
  padding: 1.2rem 1.4rem;
  border-radius: 20px;
  background: #0f172a;
  color: #e2e8f0;
  font-family: 'Fira Code', 'SFMono-Regular', Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace;
  font-size: 0.92rem;
  line-height: 1.6;
  white-space: pre-wrap;
  word-break: break-word;
  border: 1px solid rgba(148, 163, 184, 0.32);
  box-shadow: inset 0 0 0 1px rgba(148, 163, 184, 0.12);
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
  grid-template-columns: 16px 1fr;
  align-items: start;
  gap: 0.65rem;
  font-size: 0.98rem;
  line-height: 1.55;
  color: rgba(15, 23, 42, 0.78);
}

.icon {
  margin-top: 0.35rem;
  height: 10px;
  width: 10px;
  border-radius: 50%;
  background: linear-gradient(135deg, rgba(59, 130, 246, 0.9), rgba(52, 168, 83, 0.9));
  box-shadow: 0 0 0 4px rgba(59, 130, 246, 0.12);
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
  .runbook {
    grid-template-columns: 1fr;
  }

  .code-block {
    font-size: 0.9rem;
  }
}
</style>

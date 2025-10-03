<template>
  <section class="slide-shell" :class="{ active: isActive }">
    <div class="panel">
      <header class="headline-group">
        <p class="eyebrow">{{ t('slide6.kicker') }}</p>
        <h2>{{ t('slide6.title') }}</h2>
      </header>

      <p class="lede">{{ t('slide6.lede') }}</p>

      <nav class="tab-bar" role="tablist" aria-label="API endpoint tabs">
        <button
          v-for="endpoint in endpoints"
          :key="endpoint.id"
          class="tab-pill"
          type="button"
          role="tab"
          :aria-selected="activeEndpoint === endpoint.id"
          :class="{ active: activeEndpoint === endpoint.id }"
          @click="selectEndpoint(endpoint.id)"
        >
          <span class="tab-label">{{ endpoint.label }}</span>
          <span class="tab-spotlight">{{ endpoint.spotlight }}</span>
        </button>
      </nav>

      <div class="content-card" role="tabpanel">
        <header class="tab-header">
          <h3>{{ t(`slide6.${activeEndpoint}.heading`) }}</h3>
          <p>{{ t(`slide6.${activeEndpoint}.description`) }}</p>
        </header>

        <div class="code-grid">
          <article class="code-card">
            <header>
              <span class="badge">{{ t('slide6.labels.request') }}</span>
              <h4>{{ t(`slide6.${activeEndpoint}.requestTitle`) }}</h4>
            </header>
            <pre class="code-block" :aria-label="t(`slide6.${activeEndpoint}.requestAria`)"><code>{{ t(`slide6.${activeEndpoint}.request`) }}</code></pre>
          </article>

          <article class="code-card">
            <header>
              <span class="badge badge--neutral">{{ t('slide6.labels.response') }}</span>
              <h4>{{ t(`slide6.${activeEndpoint}.responseTitle`) }}</h4>
            </header>
            <pre class="code-block" :aria-label="t(`slide6.${activeEndpoint}.responseAria`)"><code>{{ t(`slide6.${activeEndpoint}.response`) }}</code></pre>
          </article>
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

type EndpointId = 'completions' | 'chat'

const endpoints = computed(() => [
  {
    id: 'completions' as const,
    label: t('slide6.tabs.completions.label'),
    spotlight: t('slide6.tabs.completions.spotlight')
  },
  {
    id: 'chat' as const,
    label: t('slide6.tabs.chat.label'),
    spotlight: t('slide6.tabs.chat.spotlight')
  }
])

const activeEndpoint = ref<EndpointId>('completions')

const selectEndpoint = (id: EndpointId) => {
  activeEndpoint.value = id
}
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
    radial-gradient(circle at 12% 18%, rgba(66, 133, 244, 0.16), transparent 58%),
    radial-gradient(circle at 88% 82%, rgba(234, 67, 53, 0.14), transparent 60%),
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

.tab-bar {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: clamp(0.6rem, 2vw, 1rem);
}

.tab-pill {
  display: flex;
  flex-direction: column;
  gap: 0.3rem;
  align-items: center;
  justify-content: center;
  padding: 1rem 2.2rem;
  border-radius: 999px;
  border: 1px solid rgba(148, 163, 184, 0.18);
  background: rgba(255, 255, 255, 0.78);
  color: #1f2937;
  font-size: 0.95rem;
  font-weight: 600;
  box-shadow: 0 14px 32px rgba(15, 23, 42, 0.08);
  cursor: pointer;
  transition: transform 220ms ease, box-shadow 220ms ease, background 220ms ease;
}

.tab-pill:hover {
  transform: translateY(-3px);
  box-shadow: 0 18px 46px rgba(66, 133, 244, 0.16);
}

.tab-pill.active {
  background: linear-gradient(135deg, rgba(66, 133, 244, 0.22), rgba(234, 67, 53, 0.25));
  color: #0f172a;
  border-color: rgba(66, 133, 244, 0.35);
}

.tab-label {
  font-size: 1rem;
  font-weight: 700;
}

.tab-spotlight {
  font-size: 0.7rem;
  letter-spacing: 0.3em;
  text-transform: uppercase;
  color: rgba(71, 85, 105, 0.72);
}

.content-card {
  width: min(100%, 1180px);
  border-radius: 30px;
  padding: clamp(1.8rem, 4vw, 2.6rem);
  background: rgba(255, 255, 255, 0.94);
  box-shadow: 0 22px 52px rgba(15, 23, 42, 0.1);
  border: 1px solid rgba(59, 130, 246, 0.18);
  display: flex;
  flex-direction: column;
  gap: clamp(1.5rem, 3vw, 2rem);
}

.tab-header {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.tab-header h3 {
  margin: 0;
  font-size: clamp(1.5rem, 3vw, 1.9rem);
  font-weight: 700;
  color: #0f172a;
}

.tab-header p {
  margin: 0;
  font-size: 1rem;
  line-height: 1.6;
  color: rgba(15, 23, 42, 0.72);
}



.code-grid {
  display: grid;
  gap: clamp(1.4rem, 3vw, 2.2rem);
  grid-template-columns: repeat(auto-fit, minmax(520px, 1fr));
}

.code-card {
  display: flex;
  flex-direction: column;
  gap: 0.9rem;
  padding: 1.5rem 1.8rem;
  border-radius: 22px;
  background: rgba(248, 250, 252, 0.94);
  border: 1px solid rgba(203, 213, 225, 0.6);
}

.code-card header {
  display: flex;
  flex-direction: column;
  gap: 0.45rem;
}

.code-card h4 {
  margin: 0;
  font-size: 1.05rem;
  font-weight: 700;
  color: rgba(15, 23, 42, 0.85);
}

.badge {
  align-self: flex-start;
  padding: 0.3rem 0.75rem;
  border-radius: 999px;
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  background: rgba(66, 133, 244, 0.14);
  color: rgba(15, 23, 42, 0.7);
}

.badge--neutral {
  background: rgba(148, 163, 184, 0.22);
}

.code-block {
  margin: 0;
  padding: 1.25rem 1.45rem;
  border-radius: 16px;
  background: #0f172a;
  color: #e2e8f0;
  font-family: 'Fira Code', 'SFMono-Regular', Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace;
  font-size: 0.96rem;
  line-height: 1.65;
  overflow-x: hidden;
  border: 1px solid rgba(148, 163, 184, 0.32);
  box-shadow: inset 0 0 0 1px rgba(148, 163, 184, 0.12);
}

.code-block code {
  white-space: pre-wrap;
  word-break: break-word;
}

@media (max-width: 960px) {
  .code-grid {
    grid-template-columns: 1fr;
  }

  .code-block {
    font-size: 0.92rem;
    overflow-x: auto;
  }
}
</style>

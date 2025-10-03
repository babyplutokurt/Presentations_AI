<script setup lang="ts">
import { ref, computed } from 'vue'

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

const tabs = computed(() => [
  {
    id: 'today',
    label: t('slide3.tabs.today.label'),
    spotlight: t('slide3.tabs.today.spotlight')
  },
  {
    id: 'requirements',
    label: t('slide3.tabs.requirements.label'),
    spotlight: t('slide3.tabs.requirements.spotlight')
  }
] as const)

type TabId = 'today' | 'requirements'

const activeTab = ref<TabId>('today')

const selectTab = (id: TabId) => {
  activeTab.value = id
}

const todayPainKeys = [
  'slide3.today.items.singleBenchmark',
  'slide3.today.items.singleThreaded'
] as const

const functionalRequirementKeys = [
  'slide3.requirements.functional.items.coverage',
  'slide3.requirements.functional.items.reporting'
] as const

const nonFunctionalRequirementKeys = [
  'slide3.requirements.nonFunctional.items.performance',
  'slide3.requirements.nonFunctional.items.scalability'
] as const

const todayPainPoints = computed(() => todayPainKeys.map(key => t(key)))
const functionalRequirements = computed(() => functionalRequirementKeys.map(key => t(key)))
const nonFunctionalRequirements = computed(() => nonFunctionalRequirementKeys.map(key => t(key)))
</script>

<template>
  <section class="slide-shell" :class="{ active: isActive }">
    <div class="panel">
      <header class="headline-group">
        <p class="eyebrow">{{ t('slide3.kicker') }}</p>
        <h2>{{ t('slide3.title') }}</h2>
      </header>

      <nav class="tab-bar" role="tablist" aria-label="Deck problem overview tabs">
        <button
          v-for="tab in tabs"
          :key="tab.id"
          class="tab-pill"
          type="button"
          role="tab"
          :aria-selected="activeTab === tab.id"
          :class="{ active: activeTab === tab.id }"
          @click="selectTab(tab.id)"
        >
          <span class="tab-label">{{ tab.label }}</span>
          <span class="tab-spotlight">{{ tab.spotlight }}</span>
        </button>
      </nav>

      <div class="tab-content" role="tabpanel">
        <div v-if="activeTab === 'today'" class="content-card">
          <h3>{{ t('slide3.today.title') }}</h3>
          <ul class="bullet-list">
            <li v-for="item in todayPainPoints" :key="item">
              <span class="bullet bullet-issue"></span>
              <span>{{ item }}</span>
            </li>
          </ul>
        </div>

        <div v-else class="content-card requirements-card">
          <h3>{{ t('slide3.requirements.title') }}</h3>

          <div class="requirement-section">
            <header class="section-header">
              <span class="badge badge-functional">{{ t('slide3.requirements.functional.title') }}</span>
            </header>
            <ul class="bullet-list">
              <li v-for="item in functionalRequirements" :key="item">
                <span class="bullet bullet-functional"></span>
                <span>{{ item }}</span>
              </li>
            </ul>
          </div>

          <div class="requirement-section">
            <header class="section-header">
              <span class="badge badge-nonfunctional">{{ t('slide3.requirements.nonFunctional.title') }}</span>
            </header>
            <ul class="bullet-list">
              <li v-for="item in nonFunctionalRequirements" :key="item">
                <span class="bullet bullet-nonfunctional"></span>
                <span>{{ item }}</span>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

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
  transform: translateY(10px);
  opacity: 0;
}

.panel {
  width: min(100%, 1080px);
  display: flex;
  flex-direction: column;
  gap: clamp(1.8rem, 4vw, 2.8rem);
  padding: clamp(1.8rem, 4vw, 3rem);
  border-radius: clamp(32px, 6vw, 48px);
  background:
    radial-gradient(circle at 12% 16%, rgba(66, 133, 244, 0.12), transparent 55%),
    radial-gradient(circle at 90% 84%, rgba(234, 67, 53, 0.08), transparent 60%),
    linear-gradient(130deg, rgba(255, 255, 255, 0.9), rgba(247, 250, 255, 0.94));
  box-shadow: 0 40px 90px rgba(15, 23, 42, 0.12);
  backdrop-filter: blur(18px);
}

.headline-group {
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
  text-align: center;
}

.headline-group h2 {
  margin: 0;
  font-size: clamp(2.2rem, 4.6vw, 3.2rem);
  font-weight: 800;
  letter-spacing: -0.02em;
  color: #111827;
}

.eyebrow {
  margin: 0;
  font-size: 0.75rem;
  font-weight: 600;
  letter-spacing: 0.55em;
  text-transform: uppercase;
  color: rgba(59, 130, 246, 0.7);
}

.tab-bar {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: clamp(0.6rem, 1.8vw, 1rem);
}

.tab-pill {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  align-items: center;
  justify-content: center;
  padding: 0.9rem 1.8rem;
  border-radius: 999px;
  border: 1px solid rgba(148, 163, 184, 0.18);
  background: rgba(255, 255, 255, 0.78);
  color: #1f2937;
  font-size: 0.9rem;
  font-weight: 600;
  box-shadow: 0 12px 26px rgba(15, 23, 42, 0.08);
  cursor: pointer;
  transition: transform 220ms ease, box-shadow 220ms ease, background 220ms ease;
}

.tab-pill:hover {
  transform: translateY(-3px);
  box-shadow: 0 18px 42px rgba(66, 133, 244, 0.16);
}

.tab-pill.active {
  background: linear-gradient(135deg, rgba(66, 133, 244, 0.22), rgba(52, 168, 82, 0.22));
  color: #0f172a;
  border-color: rgba(59, 130, 246, 0.35);
}

.tab-label {
  font-size: 0.95rem;
  font-weight: 700;
}

.tab-spotlight {
  font-size: 0.7rem;
  letter-spacing: 0.3em;
  text-transform: uppercase;
  color: rgba(71, 85, 105, 0.72);
}

.tab-content {
  width: 100%;
  display: flex;
  justify-content: center;
}

.content-card {
  width: min(100%, 760px);
  border-radius: 28px;
  padding: 2.2rem;
  background: rgba(255, 255, 255, 0.92);
  box-shadow: 0 18px 45px rgba(15, 23, 42, 0.08);
  border: 1px solid rgba(244, 114, 182, 0.25);
  min-height: clamp(24rem, 48vh, 34rem);
  display: flex;
  flex-direction: column;
}

.requirements-card {
  border-color: rgba(96, 165, 250, 0.22);
  display: flex;
  flex-direction: column;
  gap: 1.8rem;
  justify-content: space-between;
}

.requirements-card h3 {
  margin: 0;
  font-size: 1.3rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: #1d4ed8;
}

.content-card:not(.requirements-card) h3 {
  margin: 0 0 1.5rem 0;
  font-size: 1.4rem;
  font-weight: 700;
  color: #be123c;
  letter-spacing: 0.12em;
  text-transform: uppercase;
}

.bullet-list {
  list-style: none;
  margin: 0;
  padding: 0;
  display: grid;
  gap: 1rem;
  flex: 1;
}

.bullet-list li {
  display: flex;
  align-items: flex-start;
  gap: 0.9rem;
  font-size: 1.15rem;
  line-height: 1.7;
  color: rgba(15, 23, 42, 0.78);
}

.bullet {
  display: inline-flex;
  height: 0.85rem;
  width: 0.85rem;
  border-radius: 999px;
  margin-top: 0.4rem;
}

.bullet-issue {
  background: linear-gradient(135deg, #ef4444, #f97316);
}

.bullet-functional {
  background: linear-gradient(135deg, #3b82f6, #60a5fa);
}

.bullet-nonfunctional {
  background: linear-gradient(135deg, #22c55e, #34d399);
}

.badge {
  display: inline-flex;
  align-items: center;
  gap: 0.35rem;
  padding: 0.45rem 1rem;
  border-radius: 999px;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.25em;
  text-transform: uppercase;
}

.badge-functional {
  background: rgba(59, 130, 246, 0.16);
  color: #1d4ed8;
}

.badge-nonfunctional {
  background: rgba(34, 197, 94, 0.16);
  color: #15803d;
}

.section-header {
  margin-bottom: 1rem;
}

.requirement-section {
  display: flex;
  flex-direction: column;
  gap: 0.9rem;
  flex: 1;
}

@media (max-width: 768px) {
  .panel {
    padding: 1.6rem;
    border-radius: 28px;
  }

  .tab-pill {
    width: 100%;
  }

  .content-card,
  .requirement-card {
    padding: 1.6rem;
  }
}
</style>

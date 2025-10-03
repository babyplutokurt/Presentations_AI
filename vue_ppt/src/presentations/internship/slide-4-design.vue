<template>
  <section class="slide-shell" :class="{ active: isActive }">
    <div class="panel">
      <header class="headline-group">
        <p class="eyebrow">{{ t('slide4.kicker') }}</p>
        <h2>{{ t('slide4.title') }}</h2>
      </header>

      <nav class="tab-bar" role="tablist" aria-label="Design choice tabs">
        <button
          v-for="tab in approachTabs"
          :key="tab.id"
          class="tab-pill"
          type="button"
          role="tab"
          :aria-selected="activeApproach === tab.id"
          :class="{ active: activeApproach === tab.id }"
          @click="selectApproach(tab.id)"
        >
          <span class="tab-label">{{ tab.label }}</span>
          <span class="tab-spotlight">{{ tab.spotlight }}</span>
        </button>
      </nav>

      <div class="tab-panels" role="tabpanel">
        <div v-if="activeApproach === 'individual'" class="content-card individual-card">
          <header class="card-header">
            <h3>{{ t('slide4.individual.title') }}</h3>
            <p class="summary">{{ t('slide4.individual.summary') }}</p>
          </header>

          <div class="split-grid">
            <div class="list-card list-card--positive">
              <h4>{{ t('slide4.individual.prosTitle') }}</h4>
              <ul>
                <li v-for="item in individualPros" :key="item">
                  <span class="bullet bullet-positive"></span>
                  <span>{{ item }}</span>
                </li>
              </ul>
            </div>

            <div class="list-card list-card--risk">
              <h4>{{ t('slide4.individual.consTitle') }}</h4>
              <ul>
                <li v-for="item in individualCons" :key="item">
                  <span class="bullet bullet-risk"></span>
                  <span>{{ item }}</span>
                </li>
              </ul>
            </div>
          </div>
        </div>

        <div v-else-if="activeApproach === 'frameworks'" class="content-card frameworks-card">
          <header class="card-header">
            <h3>{{ t('slide4.frameworks.title') }}</h3>
          </header>

          <nav class="framework-tab-bar" role="tablist" aria-label="Framework comparison">
            <button
              v-for="framework in frameworkTabs"
              :key="framework.id"
              class="framework-tab"
              type="button"
              role="tab"
              :aria-selected="activeFramework === framework.id"
              :class="{ active: activeFramework === framework.id }"
              @click="selectFramework(framework.id)"
            >
              <span class="framework-label">{{ framework.label }}</span>
              <span v-if="framework.tag" class="framework-tag">{{ framework.tag }}</span>
            </button>
          </nav>

          <div class="framework-detail">
            <p class="detail-description">{{ frameworkDescription }}</p>

            <div class="detail-grid">
              <div class="list-card list-card--positive">
                <h4>{{ t('slide4.frameworks.detail.prosTitle') }}</h4>
                <ul>
                  <li v-for="item in frameworkPros" :key="item">
                    <span class="bullet bullet-positive"></span>
                    <span>{{ item }}</span>
                  </li>
                </ul>
              </div>

              <div class="list-card list-card--risk">
                <h4>{{ t('slide4.frameworks.detail.consTitle') }}</h4>
                <ul>
                  <li v-for="item in frameworkCons" :key="item">
                    <span class="bullet bullet-risk"></span>
                    <span>{{ item }}</span>
                  </li>
                </ul>
              </div>
            </div>

            <div class="detail-recommendation">
              <span class="label">{{ t('slide4.frameworks.detail.recommendationLabel') }}</span>
              <p>{{ frameworkRecommendation }}</p>
            </div>
          </div>
        </div>

        <div v-else class="content-card decision-card">
          <header class="card-header">
            <h3>{{ t('slide4.decision.title') }}</h3>
          </header>

          <div class="decision-callout">
            <span class="label">{{ t('slide4.decision.calloutLabel') }}</span>
            <p>{{ decisionCallout }}</p>
          </div>
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

const approachTabs = computed(() => [
  {
    id: 'individual' as const,
    label: t('slide4.tabs.individual.label'),
    spotlight: t('slide4.tabs.individual.spotlight')
  },
  {
    id: 'frameworks' as const,
    label: t('slide4.tabs.frameworks.label'),
    spotlight: t('slide4.tabs.frameworks.spotlight')
  },
  {
    id: 'decision' as const,
    label: t('slide4.tabs.decision.label'),
    spotlight: t('slide4.tabs.decision.spotlight')
  }
])

type ApproachId = 'individual' | 'frameworks' | 'decision'

const activeApproach = ref<ApproachId>('frameworks')

const selectApproach = (id: ApproachId) => {
  activeApproach.value = id
}

const individualProsKeys = [
  'slide4.individual.pros.fastStart',
  'slide4.individual.pros.noDependency'
] as const

const individualConsKeys = [
  'slide4.individual.cons.limitedCoverage',
  'slide4.individual.cons.maintenance'
] as const

const individualPros = computed(() => individualProsKeys.map(key => t(key)))
const individualCons = computed(() => individualConsKeys.map(key => t(key)))

const frameworkTabs = computed(() => [
  {
    id: 'huggingface' as const,
    label: t('slide4.frameworkTabs.huggingface.label'),
    tag: t('slide4.frameworkTabs.huggingface.tag')
  },
  {
    id: 'vertex' as const,
    label: t('slide4.frameworkTabs.vertex.label'),
    tag: t('slide4.frameworkTabs.vertex.tag')
  },
  {
    id: 'lmEval' as const,
    label: t('slide4.frameworkTabs.lmEval.label'),
    tag: t('slide4.frameworkTabs.lmEval.tag')
  },
  {
    id: 'evalchemy' as const,
    label: t('slide4.frameworkTabs.evalchemy.label'),
    tag: t('slide4.frameworkTabs.evalchemy.tag')
  }
])

type FrameworkId = 'huggingface' | 'vertex' | 'lmEval' | 'evalchemy'

const activeFramework = ref<FrameworkId>('lmEval')

const selectFramework = (id: FrameworkId) => {
  activeFramework.value = id
}

const frameworkProsKeyMap: Record<FrameworkId, readonly string[]> = {
  huggingface: [
    'slide4.frameworkTabs.huggingface.pros.customMetrics'
  ],
  vertex: [
    'slide4.frameworkTabs.vertex.pros.judger'
  ],
  lmEval: [
    'slide4.frameworkTabs.lmEval.pros.coverage',
    'slide4.frameworkTabs.lmEval.pros.ecosystem'
  ],
  evalchemy: [
    'slide4.frameworkTabs.evalchemy.pros.math',
    'slide4.frameworkTabs.evalchemy.pros.extension'
  ]
} as const

const frameworkConsKeyMap: Record<FrameworkId, readonly string[]> = {
  huggingface: [
    'slide4.frameworkTabs.huggingface.cons.manual',
    'slide4.frameworkTabs.huggingface.cons.automation'
  ],
  vertex: [
    'slide4.frameworkTabs.vertex.cons.inhouse',
    'slide4.frameworkTabs.vertex.cons.dependency'
  ],
  lmEval: [
    'slide4.frameworkTabs.lmEval.cons.integration'
  ],
  evalchemy: [
    'slide4.frameworkTabs.evalchemy.cons.dependency'
  ]
} as const

const frameworkPros = computed(() => frameworkProsKeyMap[activeFramework.value].map(key => t(key)))
const frameworkCons = computed(() => frameworkConsKeyMap[activeFramework.value].map(key => t(key)))

const frameworkDescription = computed(() => t(`slide4.frameworkTabs.${activeFramework.value}.description`))
const frameworkRecommendation = computed(() => t(`slide4.frameworkTabs.${activeFramework.value}.recommendation`))

const decisionPhases = computed(() => [
  {
    label: t('slide4.decision.phases.phase1.label'),
    detail: t('slide4.decision.phases.phase1.detail')
  },
  {
    label: t('slide4.decision.phases.phase2.label'),
    detail: t('slide4.decision.phases.phase2.detail')
  },
  {
    label: t('slide4.decision.phases.phase3.label'),
    detail: t('slide4.decision.phases.phase3.detail')
  }
])

const decisionNextStepKeys = [
  'slide4.decision.nextSteps.alignStakeholders',
  'slide4.decision.nextSteps.buildServer',
  'slide4.decision.nextSteps.prepareEval',
  'slide4.decision.nextSteps.lmEvalPR'
] as const

const decisionNextSteps = computed(() => decisionNextStepKeys.map(key => t(key)))
const decisionCallout = computed(() => t('slide4.decision.callout'))
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
  width: min(100%, 1120px);
  display: flex;
  flex-direction: column;
  gap: clamp(1.8rem, 4vw, 2.6rem);
  padding: clamp(1.9rem, 4vw, 3.1rem);
  border-radius: clamp(32px, 6vw, 48px);
  background:
    radial-gradient(circle at 14% 18%, rgba(66, 133, 244, 0.16), transparent 58%),
    radial-gradient(circle at 86% 82%, rgba(52, 168, 83, 0.12), transparent 60%),
    linear-gradient(135deg, rgba(255, 255, 255, 0.94), rgba(246, 248, 255, 0.96));
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
  font-size: clamp(2.1rem, 4.2vw, 2.9rem);
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
  background: linear-gradient(135deg, rgba(66, 133, 244, 0.22), rgba(250, 187, 5, 0.25));
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

.tab-panels {
  width: 100%;
  display: flex;
  justify-content: center;
}

.content-card {
  width: min(100%, 860px);
  border-radius: 30px;
  padding: clamp(1.8rem, 4vw, 2.6rem);
  background: rgba(255, 255, 255, 0.94);
  box-shadow: 0 22px 52px rgba(15, 23, 42, 0.1);
  border: 1px solid rgba(59, 130, 246, 0.18);
  display: flex;
  flex-direction: column;
  gap: clamp(1.5rem, 3vw, 2rem);
}

.individual-card {
  border-color: rgba(248, 113, 113, 0.22);
}

.frameworks-card {
  border-color: rgba(59, 130, 246, 0.24);
}

.card-header h3 {
  margin: 0;
  font-size: clamp(1.5rem, 3.2vw, 2rem);
  font-weight: 700;
  color: #1e3a8a;
  text-transform: uppercase;
  letter-spacing: 0.12em;
}

.card-header .summary {
  margin: 0.75rem 0 0;
  font-size: 1.05rem;
  line-height: 1.6;
  color: rgba(15, 23, 42, 0.72);
}

.split-grid {
  display: grid;
  gap: 1.5rem;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
}

.list-card {
  border-radius: 24px;
  padding: 1.6rem;
  background: rgba(248, 250, 252, 0.92);
  border: 1px solid rgba(148, 163, 184, 0.18);
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.list-card h4 {
  margin: 0;
  font-size: 1rem;
  letter-spacing: 0.25em;
  text-transform: uppercase;
  color: #1f2937;
}

.list-card ul {
  margin: 0;
  padding: 0;
  list-style: none;
  display: grid;
  gap: 0.9rem;
}

.list-card li {
  display: flex;
  gap: 0.9rem;
  font-size: 1.02rem;
  line-height: 1.6;
  color: rgba(15, 23, 42, 0.78);
}

.list-card--positive {
  background: rgba(219, 234, 254, 0.6);
  border-color: rgba(59, 130, 246, 0.25);
}

.list-card--risk {
  background: rgba(254, 226, 226, 0.6);
  border-color: rgba(248, 113, 113, 0.25);
}

.bullet {
  display: inline-flex;
  height: 0.85rem;
  width: 0.85rem;
  border-radius: 999px;
  margin-top: 0.35rem;
}

.bullet-positive {
  background: linear-gradient(135deg, #38bdf8, #2563eb);
}

.bullet-risk {
  background: linear-gradient(135deg, #f97316, #ef4444);
}
.framework-tab-bar {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 0.75rem;
}

.framework-tab {
  display: flex;
  flex-direction: column;
  gap: 0.35rem;
  align-items: flex-start;
  justify-content: center;
  padding: 1rem 1.4rem;
  border-radius: 20px;
  border: 1px solid rgba(148, 163, 184, 0.2);
  background: rgba(255, 255, 255, 0.86);
  color: #1e293b;
  font-size: 0.95rem;
  font-weight: 600;
  box-shadow: 0 14px 30px rgba(15, 23, 42, 0.08);
  cursor: pointer;
  transition: transform 200ms ease, box-shadow 200ms ease, border-color 200ms ease;
}

.framework-tab .framework-tag {
  display: inline-flex;
  align-items: center;
  padding: 0.2rem 0.6rem;
  border-radius: 999px;
  background: rgba(59, 130, 246, 0.1);
  color: #1d4ed8;
  font-size: 0.7rem;
  letter-spacing: 0.14em;
  text-transform: uppercase;
}

.framework-tab:hover {
  transform: translateY(-2px);
  box-shadow: 0 18px 42px rgba(59, 130, 246, 0.18);
}

.framework-tab.active {
  border-color: rgba(37, 99, 235, 0.4);
  background: linear-gradient(135deg, rgba(191, 219, 254, 0.6), rgba(221, 214, 254, 0.6));
  color: #0f172a;
}

.framework-detail {
  display: flex;
  flex-direction: column;
  gap: 1.4rem;
}

.detail-description {
  margin: 0;
  font-size: 1rem;
  line-height: 1.7;
  color: rgba(30, 41, 59, 0.84);
}

.detail-grid {
  display: grid;
  gap: 1.2rem;
  grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
}

.detail-recommendation {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
  padding: 1rem 1.4rem;
  border-radius: 18px;
  background: rgba(224, 231, 255, 0.7);
  border: 1px solid rgba(99, 102, 241, 0.3);
  color: #312e81;
}

.detail-recommendation .label {
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.28em;
  font-weight: 700;
}

.detail-recommendation p {
  margin: 0;
  font-size: 0.98rem;
  line-height: 1.6;
}

.bullet-decision {
  background: linear-gradient(135deg, #22d3ee, #14b8a6);
}

.decision-card {
  border-color: rgba(45, 212, 191, 0.35);
}

.decision-grid {
  display: grid;
  gap: 1.5rem;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
}

.decision-list {
  background: rgba(224, 255, 249, 0.75);
  border-color: rgba(13, 148, 136, 0.28);
}

.decision-list ul {
  padding: 0;
  margin: 0;
  list-style: none;
}

.decision-list--phases ul {
  display: grid;
  gap: 1rem;
}

.decision-phase {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
  font-size: 1rem;
  color: rgba(15, 23, 42, 0.82);
}

.decision-list--steps ul {
  display: grid;
  gap: 0.75rem;
}

.decision-step {
  display: flex;
  align-items: flex-start;
  gap: 0.8rem;
  font-size: 1.02rem;
  line-height: 1.6;
  color: rgba(15, 23, 42, 0.82);
}

.decision-step .bullet {
  margin-top: 0.25rem;
}

.phase-label {
  font-size: 0.78rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.22em;
  color: #0f766e;
}

.phase-detail {
  font-size: 1.02rem;
  line-height: 1.6;
}

.decision-callout {
  padding: 1.4rem 1.6rem;
  border-radius: 22px;
  background: linear-gradient(135deg, rgba(56, 189, 248, 0.18), rgba(16, 185, 129, 0.24));
  border: 1px solid rgba(56, 189, 248, 0.3);
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
  color: #0f172a;
}

.decision-callout .label {
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.3em;
  text-transform: uppercase;
}

.decision-callout p {
  margin: 0;
  font-size: 1.05rem;
  line-height: 1.7;
}

@media (max-width: 768px) {
  .panel {
    padding: 1.6rem;
    border-radius: 28px;
  }

  .tab-pill {
    width: 100%;
  }

  .content-card {
    padding: 1.6rem;
  }

  .framework-tab-bar {
    grid-template-columns: 1fr;
  }

  .decision-grid {
    grid-template-columns: 1fr;
  }
}
</style>

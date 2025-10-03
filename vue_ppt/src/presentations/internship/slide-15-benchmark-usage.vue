<template>
  <section class="slide-shell" :class="{ active: isActive }">
    <div class="panel">
      <header class="headline-group">
        <p class="eyebrow">{{ t('slide15.kicker') }}</p>
        <h2>{{ t('slide15.title') }}</h2>
      </header>

      <p class="lede">{{ t('slide15.lede') }}</p>

      <ul class="achievement-list">
        <li v-for="item in achievements" :key="item.title" class="achievement">
          <span class="icon"></span>
          <div>
            <h3>{{ item.title }}</h3>
            <p>{{ item.body }}</p>
          </div>
        </li>
      </ul>
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

const achievementKeys = [
  {
    title: 'slide15.achievements.coverageTitle',
    body: 'slide15.achievements.coverageBody'
  },
  {
    title: 'slide15.achievements.speedTitle',
    body: 'slide15.achievements.speedBody'
  },
  {
    title: 'slide15.achievements.apiTitle',
    body: 'slide15.achievements.apiBody'
  },
  {
    title: 'slide15.achievements.validationTitle',
    body: 'slide15.achievements.validationBody'
  }
] as const

const achievements = computed(() =>
  achievementKeys.map(item => ({
    title: t(item.title),
    body: t(item.body)
  }))
)
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
  width: min(100%, 1240px);
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

.achievement-list {
  margin: 0;
  padding: 0;
  list-style: none;
  display: grid;
  gap: clamp(1.2rem, 2.4vw, 1.8rem);
}

.achievement {
  display: grid;
  grid-template-columns: 16px 1fr;
  gap: 0.8rem;
  padding: clamp(1.4rem, 2.6vw, 2rem);
  border-radius: 28px;
  background: rgba(255, 255, 255, 0.94);
  border: 1px solid rgba(148, 163, 184, 0.18);
  box-shadow: 0 18px 42px rgba(15, 23, 42, 0.1);
}

.icon {
  margin-top: 0.4rem;
  height: 10px;
  width: 10px;
  border-radius: 50%;
  background: linear-gradient(135deg, rgba(59, 130, 246, 0.85), rgba(52, 168, 83, 0.85));
  box-shadow: 0 0 0 4px rgba(59, 130, 246, 0.12);
}

.achievement h3 {
  margin: 0;
  font-size: clamp(1.2rem, 2.4vw, 1.6rem);
  font-weight: 700;
  color: #0f172a;
}

.achievement p {
  margin: 0.35rem 0 0;
  font-size: 0.98rem;
  line-height: 1.6;
  color: rgba(15, 23, 42, 0.78);
}
</style>

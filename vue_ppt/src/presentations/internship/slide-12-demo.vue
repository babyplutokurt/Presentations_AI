<template>
  <section class="slide-shell" :class="{ active: isActive }">
    <div class="panel">
      <p class="eyebrow">{{ t('slide12.kicker') }}</p>
      <h2>{{ t('slide12.title') }}</h2>
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
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  padding: clamp(2.4rem, 5vw, 3.6rem);
  border-radius: clamp(36px, 7vw, 56px);
  background:
    radial-gradient(circle at 20% 20%, rgba(66, 133, 244, 0.18), transparent 58%),
    radial-gradient(circle at 80% 80%, rgba(251, 188, 5, 0.16), transparent 60%),
    linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(243, 249, 255, 0.96));
  box-shadow: 0 45px 90px rgba(15, 23, 42, 0.14);
  backdrop-filter: blur(18px);
}

.eyebrow {
  margin: 0;
  font-size: 0.78rem;
  font-weight: 600;
  letter-spacing: 0.55em;
  text-transform: uppercase;
  color: rgba(66, 133, 244, 0.7);
}

h2 {
  margin: 0;
  font-size: clamp(3rem, 6vw, 4.2rem);
  font-weight: 800;
  letter-spacing: -0.02em;
  color: #0f172a;
}
</style>

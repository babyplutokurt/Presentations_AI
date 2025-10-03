<template>
  <div class="soft-mesh-background" aria-hidden="true">
    <div class="layer mesh-gradient" />
    <div class="glass-veil" />
  </div>
</template>

<script setup lang="ts">
// No script needed; purely visual background.
</script>

<style scoped>
.soft-mesh-background {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 0;
}

.layer {
  position: absolute;
  inset: 0;
}

.mesh-gradient {
  background-image:
    radial-gradient(900px 520px at 15% 22%, rgba(66, 133, 244, 0.5), transparent 60%),
    radial-gradient(820px 480px at 82% 28%, rgba(234, 67, 53, 0.46), transparent 60%),
    radial-gradient(760px 520px at 32% 82%, rgba(250, 187, 5, 0.44), transparent 65%),
    radial-gradient(780px 520px at 75% 78%, rgba(52, 168, 82, 0.46), transparent 60%),
    linear-gradient(180deg, #ffffff, #f7f9ff 45%, rgba(247, 249, 255, 0.65));
  filter: saturate(1.05) contrast(1.02);
}

.glass-veil {
  position: absolute;
  inset: 0;
  background: rgba(255, 255, 255, 0.12);
  backdrop-filter: blur(4px) saturate(1.02);
  -webkit-backdrop-filter: blur(4px) saturate(1.02);
  pointer-events: none;
}
</style>

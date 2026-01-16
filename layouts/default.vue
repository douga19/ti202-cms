<template>
  <div class="slidev-layout">
    <slot />

    <footer
      v-if="$nav.currentLayout !== 'cover'"
      class="page-number"
    >
      {{ $nav.currentPage }} / {{ $nav.total }}
    </footer>
  </div>
</template>

<style scoped>
.page-number {
  position: fixed;
  bottom: 0.5rem;
  right: 1rem;
  font-size: 0.7rem;
  opacity: 0.6;
}
</style>

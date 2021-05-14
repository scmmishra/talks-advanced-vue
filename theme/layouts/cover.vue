<template>
  <div class="cover">
    <div class="mb-24">
      <slot />
    </div>
  </div>
</template>

<style>
.cover {
  @apply flex h-full items-center;
}

.cover h1 {
  @apply text-6xl;
}

.cover h1 + p {
  @apply text-2xl mt-2;
}
</style>

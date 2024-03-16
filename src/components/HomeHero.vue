<script setup>
defineProps({
  title: {
    type: String,
    required: true,
  },
});
</script>
<template>
  <div>
    <h1 class="hero-title">{{ title }}</h1>
  </div>
</template>

<style lang="scss" scoped></style>

<script>
export default {
  props: {
    prev: {
      type: Object,
      default: () => null
    },
    next: {
      type: Object,
      default: () => null
    },
    category: {
      type: String,
      required: true
    }
  }
}
</script>


<template>
  <div class="flex justify-between">
    <NuxtLink
      v-if="prev"
      :to="`/articles/${category}/${prev.slug}`"
      class="button"
    >
      ← {{ prev.title }}
    </NuxtLink>
    <span v-else>&nbsp;</span>
    <NuxtLink
      v-if="next"
      :to="`/articles/${category}/${next.slug}`"
      class="button"
    >
      {{ next.title }} →
    </NuxtLink>
    <span v-else>&nbsp;</span>
  </div>
</template>

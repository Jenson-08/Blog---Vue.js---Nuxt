<script>
export default {
  async asyncData({ $content, params, error }) {
    const category = params.category

    try {
      const articles = await $content(`articles/${category}`)
        .only(['title', 'slug'])
        .sortBy('createdAt', 'asc')
        .fetch()

      return {
        category,
        articles
      }
    } catch (err) {
      return error({ statusCode: 404, message: `Categoría "${category}" no encontrada` })
    }
  }
}

</script>


<template>
  <div class="container">
    <h1>Artículos de la categoría "{{ category }}"</h1>

    <ul>
      <li v-for="article in articles" :key="article.slug">
        <NuxtLink :to="`/articles/${category}/${article.slug}`">
            {{ article.title }}
        </NuxtLink>

      </li>
    </ul>

    <NuxtLink to="/">← Volver al inicio</NuxtLink>
  </div>
</template>

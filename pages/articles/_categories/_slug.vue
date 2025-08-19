<script>
export default {
  async asyncData({ $content, params, error }) {
    const { categories, slug } = params

    // Busca el artículo dentro de esa categoría
    const articles = await $content(`articles/${categories}`)
      .where({ slug })
      .fetch()

    const article = articles.length ? articles[0] : null

    if (!article) {
      return error({ statusCode: 404, message: 'Artículo no encontrado' })
    }

    // Buscar prev y next dentro de la misma categoría
    const [prev, next] = await $content(`articles/${categories}`)
      .only(['title', 'slug'])
      .sortBy('createdAt', 'asc')
      .surround(slug)
      .fetch()

    return {
      article,
      prev,
      next,
      categories,
      slug
    }
  },
methods: {
  formatDate(date) {
    if (!date) return 'Fecha no disponible'
    const d = new Date(date)
    if (isNaN(d)) return 'Fecha inválida'
    return d.toLocaleDateString('es-ES', {
      year: 'numeric',
      month: 'long',
      day: 'numeric'
    })
  }
}
}

</script>

<template>
  <div class="container">
   <article class="row">
      <h1>{{ article.title }}</h1>
      <p>{{ article.description }}</p>
      <img v-if="article.img" :src="article.img" :alt="article.alt" />
      <p>Fecha de creación: {{ formatDate(article.createdAt) }}</p>
      

      <nuxt-content :document="article" />

      <p>Última actualización: {{ formatDate(article.updatedAt) }}</p>


      <author v-if="article.author" :author="article.author" />
      <prev-next :prev="prev" :next="next" :category="categories" />
      <NuxtLink :to="`/articles/${categories}`">← Volver a la categoría</NuxtLink>

    </article>
  </div>
</template>


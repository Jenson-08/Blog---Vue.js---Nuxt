<script>
import SiteHeader from '@/components/global/SiteHeader.vue'
import SiteFooter from '@/components/global/SiteFooter.vue'
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
    <div>
    <!-- Header fuera del container -->
    <SiteHeader />
    <div class="container">
      <h1>Articles in the category {{ category }}</h1>

      <ul class="article-list">
        <li v-for="article in articles" :key="article.slug" class="article-card">
          <NuxtLink :to="`/articles/${category}/${article.slug}`">
              {{ article.title }}
          </NuxtLink>

        </li>
      </ul>

      <NuxtLink to="/" class="nav-link">← Volver al inicio</NuxtLink>
    </div>
   <SiteFooter />
  </div>
</template>

<style scoped>
h1 {
  text-align: center;
  margin-top: 4rem;
  margin-bottom: 4rem;
  font-size: 4rem;
  color: #333;
}

/* Lista sin viñetas */
.article-list {
  list-style:circle;
  padding: 0;
  margin: 0;
}

/* Estilo tipo tarjeta */
.article-card {
  background: #f9f9f9;
  margin-bottom: 1rem;
  padding: 1rem 1.5rem;
  border-radius: 6px;
  border: 1px solid #eee;
  transition: box-shadow 0.3s ease;
}

.article-card:hover {
  background-color: #5081ea;
  color: #fff;
}

.article-card a {
  text-decoration: none;
  color: #333;
  font-weight: 600;
  display: block;
  font-size: 1.2rem;
}

/* Link de volver al inicio */
.back-link {
  display: inline-block;
  margin-top: 2rem;
  text-decoration: none;
  color: #1EAEDB;
  font-weight: 500;
  transition: color 0.3s;
}

.back-link:hover {
  color: #0077aa;
}
.nav-link {
  margin-left: 0; /* reset if needed */
  color: #333;
  font-weight: 600;
  text-decoration: none;
  padding: 0.4rem 0.8rem;
  border-radius: 4px;
  transition: background-color 0.3s;
  display: inline-block;
}

.nav-link:hover {
  background-color: #5081ea;
  color: #fff;
}

</style>
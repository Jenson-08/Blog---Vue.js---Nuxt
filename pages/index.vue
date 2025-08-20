<template>
  <div>
    <!-- Header fuera del container -->
    <SiteHeader />

    <div class="container">
      <div class="row main-content">
        <h2>Blog Categories</h2>

        <nav class="categories-nav">
          <div class="category-item">
            <NuxtLink to="/articles/events">Events</NuxtLink>
            <img src="/images/events1.jpg" alt="Events" class="category-image" />
          </div>
          <div class="category-item">
            <NuxtLink to="/articles/spectacles">Spectacles</NuxtLink>
            <img src="/images/spect2.jpeg" alt="Spectacles" class="category-image" />
          </div>
          <div class="category-item">
            <NuxtLink to="/articles/sports">Sports</NuxtLink>
            <img src="/images/sports3.png" alt="Sports" class="category-image"/>
          </div>
        </nav>

        <ul class="article-list">
          <li v-for="article of articles" :key="article.slug" class="article-card">
            <NuxtLink :to="{ name: 'blog-slug', params: { slug: article.slug } }">
              <div>
                <h3>{{ article.title }}</h3>
                <p>{{ article.description }}</p>
              </div>
            </NuxtLink>
          </li>
        </ul>
      </div>
    </div>

    <!-- Footer fuera del container -->
    <SiteFooter />
  </div>
</template>


<script>
import SiteHeader from '@/components/global/SiteHeader.vue'
import SiteFooter from '@/components/global/SiteFooter.vue'

export default {
  components: {
    SiteHeader,
    SiteFooter
  },
  async asyncData({ $content }) {
    const articles = await $content('articles')
        .only(['title', 'slug'])
        .sortBy('createdAt', 'asc')
        .fetch()
    return { articles }
  }
}
</script>

<style scoped>
/* Aquí van tus estilos para index.vue (categories-nav, article-list, etc.) */

/* Mantén los estilos generales */
.category-image {
  width: 180px !important;
  height: 120px !important;
  object-fit: cover !important;
  border-radius: 8px;
  margin-top: 0.8rem;
  display: block;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}


.categories-nav {
  margin-bottom: 2rem;
  display: flex;
  justify-content: center;    /* Centrar horizontalmente */
  gap: 3rem;                  /* Espacio entre categorías */
  flex-wrap: wrap;            /* Para que se adapten en pantallas pequeñas */
}

.category-item {
  display: flex;
  flex-direction: column;     /* Apilar link e imagen verticalmente */
  align-items: center;        /* Centrar contenido */
  cursor: pointer;
  width: 180px;               /* Ancho fijo para uniformidad */
}

.category-item a {
  padding: 0.6rem 1.2rem;
  background-color: #6a6d6d !important;
  border-radius: 6px;
  text-decoration: none;
  color: #fff !important;
  font-weight: 600;
  font-size: 1.3rem;
  text-align: center;
  width: 100%;
  transition: background-color 0.3s, color 0.3s;
}

.category-item a:hover {
  background-color: #555 !important;
  color: #5081ea !important;
}

.category-item img {
  margin-top: 0.8rem;
  width: 100%;
  height: auto;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(194, 21, 21, 0.1);
  object-fit: cover;
}
.article-list { list-style: none; padding: 0; }
.article-card { margin-bottom: 1.5rem; padding: 1rem; border: 1px solid #eee; border-radius: 5px; transition: box-shadow 0.3s; }
.article-card:hover { box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05); } 
.article-card h3 { margin: 0 0 0.5rem 0; font-size: 1.4rem; } 
.article-card p { margin: 0; color: #da2222; } 
.article-card a { text-decoration: none; color: inherit; display: block; } 
.main-content h2 { text-align: center; margin-bottom: 1.5rem; }
</style>

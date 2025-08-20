<template>
  <header class="site-header">
    <h1 class="site-title">The UNA Times</h1>
    <nav class="main-nav">
      <NuxtLink to="/">Home</NuxtLink>
      <NuxtLink to="/about">About</NuxtLink>
      <NuxtLink to="/contact">Contact</NuxtLink>
    </nav>
  </header>
</template>

<style scoped>
.site-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 0;
  border-bottom: 1px solid #699fec;
  margin-bottom: 2rem;
}

.site-title {
  font-size: 2rem;
  margin: 0;
  color: #333;
}

.main-nav a {
  margin-left: 1.2rem;
  color: #333;
  font-weight: 600;
  text-decoration: none;
  padding: 0.4rem 0.8rem;
  border-radius: 4px;
  transition: background-color 0.3s;
}

.main-nav a:hover {
  background-color: #5081ea;
}
</style>

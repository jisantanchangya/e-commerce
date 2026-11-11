<script setup>
import heroImage from '@/assets/images/home_hero.webp'
</script>

<template>
  <section class="home-hero">
    <img class="hero-image" :src="heroImage" alt="" />
    <div class="hero-overlay"></div>
    <div class="hero-content">
      <h1 class="hero-title">Welcome to Our Store</h1>
      <p class="hero-subtitle">Discover the best products at unbeatable prices.</p>
      <router-link class="hero-button" to="/shop">Shop Now</router-link>
    </div>
  </section>
</template>

<style scoped>
.home-hero {
  position: relative;
  display: grid;
  min-height: 100vh;
  min-height: 100svh;
  place-items: center;
  overflow: hidden;
  background: #262626;
  color: #fff;
  text-align: center;
}

.hero-image,
.hero-overlay {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
}

.hero-image {
  object-fit: cover;
  object-position: center;
}

.hero-overlay {
  background: linear-gradient(90deg, rgb(0 0 0 / 48%), rgb(0 0 0 / 12%));
}

.hero-content {
  position: relative;
  z-index: 1;
  max-width: 680px;
  padding: 2rem;
}

.hero-title {
  margin: 0;
  font-size: clamp(2.5rem, 6vw, 5rem);
  font-weight: 600;
  letter-spacing: -0.04em;
  line-height: 1.05;
}

.hero-subtitle {
  margin: 1.25rem 0 2rem;
  font-size: clamp(1rem, 2vw, 1.2rem);
  line-height: 1.6;
}

.hero-button {
  display: inline-flex;
  min-height: 48px;
  align-items: center;
  justify-content: center;
  padding: 0 1.75rem;
  background: #fff;
  color: #202020;
  font-size: 0.8rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  text-decoration: none;
  text-transform: uppercase;
  transition: background-color 160ms ease;
}

.hero-button:hover {
  background: #e8e8e8;
}
</style>

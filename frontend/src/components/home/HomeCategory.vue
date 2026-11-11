<script setup>
import bestSellersImage from '@/assets/images/best_sellers.webp'
import menImage from '@/assets/images/men.webp'
import newArrivalImage from '@/assets/images/new_arrival.webp'
import womenImage from '@/assets/images/women.webp'

const categories = [
  { name: 'NEW ARRIVALS', image: newArrivalImage },
  { name: 'MEN', image: menImage },
  { name: 'WOMEN', image: womenImage },
  { name: 'BEST SELLERS', image: bestSellersImage },
]
</script>

<template>
  <section class="home-category" aria-label="Shop by category">
    <div class="category-container">
      <div
        v-for="category in categories"
        :key="category.name"
        class="category-item"
      >
        <img :src="category.image" :alt="category.name" />
        <span class="category-overlay"></span>
        <h2>{{ category.name }}</h2>
      </div>
    </div>
  </section>
</template>

<style scoped>
.home-category {
  padding: 3rem 0;
  background: #fff;
}

.category-container {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 1.25rem;
  max-width: 1440px;
  margin: 0 auto;
  padding: 0 2.25rem;
}

.category-item {
  position: relative;
  display: block;
  overflow: hidden;
  aspect-ratio: 3 / 4;
  background: #eee;
  color: #fff;
  text-decoration: none;
}

.category-item img,
.category-overlay {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
}

.category-item img {
  object-fit: cover;
  transition: transform 350ms ease;
}

.category-item:hover img {
  transform: scale(1.04);
}

.category-overlay {
  background: linear-gradient(180deg, transparent 45%, rgb(0 0 0 / 48%));
}

.category-item h2 {
  position: absolute;
  bottom: 1.5rem;
  left: 50%;
  width: max-content;
  max-width: calc(100% - 1.5rem);
  margin: 0;
  padding: 0.8rem 1.2rem;
  border: 1px solid transparent;
  border-radius: 999px;
  font-size: clamp(0.9rem, 1.4vw, 1.2rem);
  font-weight: 600;
  letter-spacing: 0.1em;
  text-align: center;
  transition:
    bottom 250ms ease,
    transform 250ms ease,
    border-color 250ms ease;
  transform: translateX(-50%);
}

.category-item:hover h2 {
  bottom: 50%;
  border-color: currentColor;
  transform: translate(-50%, 50%);
}

@media (max-width: 960px) {
  .category-container {
    grid-template-columns: repeat(2, minmax(0, 1fr));
    padding: 0 1.25rem;
  }
}

@media (max-width: 600px) {
  .home-category {
    padding: 1.5rem 0;
  }

  .category-container {
    gap: 0.75rem;
  }
}
</style>

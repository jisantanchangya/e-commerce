<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

const trendingImages = Object.entries(
  import.meta.glob('../../assets/images/men_trending/*', {
    eager: true,
    import: 'default',
  }),
)
  .sort(([first], [second]) => first.localeCompare(second))
  .map(([, image]) => image)

const carousel = ref(null)
let autoplay

function moveNext() {
  const track = carousel.value
  if (!track) return

  const lastScroll = track.scrollWidth - track.clientWidth
  if (track.scrollLeft >= lastScroll - 1) {
    track.scrollTo({ left: 0, behavior: 'smooth' })
    return
  }

  const firstItem = track.firstElementChild
  const gap = Number.parseFloat(getComputedStyle(track).columnGap) || 0
  track.scrollBy({
    left: (firstItem?.getBoundingClientRect().width || 0) + gap,
    behavior: 'smooth',
  })
}

function movePrevious() {
  const track = carousel.value
  if (!track) return

  if (track.scrollLeft <= 1) {
    track.scrollTo({ left: track.scrollWidth - track.clientWidth, behavior: 'smooth' })
    return
  }

  const firstItem = track.firstElementChild
  const gap = Number.parseFloat(getComputedStyle(track).columnGap) || 0
  track.scrollBy({
    left: -((firstItem?.getBoundingClientRect().width || 0) + gap),
    behavior: 'smooth',
  })
}

onMounted(() => {
  autoplay = window.setInterval(moveNext, 3000)
})
onUnmounted(() => {
  window.clearInterval(autoplay)
})
</script>

<template>
  <section class="men-trending" aria-labelledby="men-trending-title">
    <div class="trending-heading">
      <h2 id="men-trending-title">Men's Trending</h2>
      <div class="carousel-controls">
        <button type="button" aria-label="Scroll to previous products" @click="movePrevious">
          <span aria-hidden="true">&larr;</span>
        </button>
        <button type="button" aria-label="Scroll to next products" @click="moveNext">
          <span aria-hidden="true">&rarr;</span>
        </button>
      </div>
    </div>

    <div
      ref="carousel"
      class="trending-carousel"
      role="group"
      aria-label="Men's trending product images"
    >
      <div v-for="(image, index) in trendingImages" :key="image" class="trending-item">
        <img :src="image" :alt="`Men's trending product ${index + 1}`" />
      </div>
    </div>
  </section>
</template>

<style scoped>
.men-trending {
  max-width: 1440px;
  margin: 0 auto;
  padding: 3rem 2.25rem;
  color: #202020;
}

.trending-heading {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 1.25rem;
}

.trending-heading h2 {
  margin: 0;
  font-size: clamp(1.5rem, 2.5vw, 2rem);
  font-weight: 600;
}

.carousel-controls {
  display: flex;
  gap: 0.5rem;
}

.carousel-controls button {
  display: grid;
  width: 2.5rem;
  height: 2.5rem;
  place-items: center;
  border: 1px solid #d8d8d8;
  border-radius: 50%;
  background: #fff;
  color: inherit;
  cursor: pointer;
  font-size: 1.25rem;
}

.carousel-controls button:hover {
  background: #f3f3f3;
}

.trending-carousel {
  display: flex;
  gap: 1rem;
  overflow-x: auto;
  scroll-behavior: smooth;
  scroll-snap-type: x mandatory;
  scrollbar-width: none;
}

.trending-carousel::-webkit-scrollbar {
  display: none;
}

.trending-item {
  flex: 0 0 calc((100% - 3rem) / 4);
  overflow: hidden;
  aspect-ratio: 3 / 4;
  background: #f5f5f5;
  scroll-snap-align: start;
}

.trending-item img {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

@media (max-width: 700px) {
  .men-trending {
    padding: 2rem 1.25rem;
  }

  .trending-item {
    flex-basis: calc((100% - 1rem) / 2);
  }
}
</style>

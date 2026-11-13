<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

const arrivalImages = Object.entries(
  import.meta.glob('../../assets/images/new_arrive/*', {
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
    track.scrollTo({ left: track.scrollWidth, behavior: 'smooth' })
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
  <section class="new-arrivals" aria-labelledby="new-arrivals-title">
    <div class="arrivals-heading">
      <h2  id="new-arrivals-title">NEW ARRIVALS</h2>
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
      class="arrivals-carousel"
      role="group"
      aria-label="New arrival product images"
    >
      <div v-for="(image, index) in arrivalImages" :key="image" class="arrival-item">
        <img :src="image" :alt="`New arrival ${index + 1}`" />
      </div>
    </div>
  </section>
</template>

<style scoped>
.new-arrivals {
  max-width: 1440px;
  margin: 0 auto;
  padding: 3rem 2.25rem;
  color: #202020;
}

.arrivals-heading {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 1.25rem;
}

.arrivals-heading h2 {
  margin: 0;
  font-size: clamp(1.5rem, 2.5vw, 2rem);
  font-weight: 200;
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

.arrivals-carousel {
  display: flex;
  gap: 1rem;
  overflow-x: auto;
  scroll-behavior: smooth;
  scroll-snap-type: x mandatory;
  scrollbar-width: none;
}

.arrivals-carousel::-webkit-scrollbar {
  display: none;
}

.arrival-item {
  flex: 0 0 calc((100% - 3rem) / 4);
  overflow: hidden;
  aspect-ratio: 3 / 4;
  background: #f5f5f5;
  scroll-snap-align: start;
}

.arrival-item img {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

@media (max-width: 700px) {
  .new-arrivals {
    padding: 2rem 1.25rem;
  }

  .arrival-item {
    flex-basis: calc((100% - 1rem) / 2);
  }
}
</style>

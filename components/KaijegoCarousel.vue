<template>
  <div class="carousel-container">
    <h4 class="carousel-title">
      Around the World with Alma Asinobi – Visual Journey
    </h4>

    <div class="carousel-wrapper" @mouseenter="pause" @mouseleave="resume">
      <button class="nav-btn prev" @click="prev">‹</button>

      <div class="carousel-viewport">
        <div
          class="carousel-track"
          :style="{
            transform: `translateX(-${currentSlide * (100 / slidesPerView)}%)`
          }"
        >
          <div
            v-for="n in totalSlides"
            :key="n"
            class="carousel-slide"
          >
            <img
              :src="`/images/projects/kaijego/a4-${n}.png`"
              :alt="`Kajego spread ${n}`"
              class="carousel-image"
              loading="lazy"
            />
          </div>
        </div>
      </div>

      <button class="nav-btn next" @click="next">›</button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

const currentSlide = ref(0)
const totalSlides = 16
let interval = null

const slidesPerView = computed(() => {
  if (process.client) {
    const w = window.innerWidth
    if (w >= 1024) return 4
    if (w >= 768) return 3
    if (w >= 640) return 2
    return 1
  }
  return 4 // Default for SSR
})

function next() {
  const max = totalSlides - slidesPerView.value
  currentSlide.value = currentSlide.value < max ? currentSlide.value + 1 : 0
}

function prev() {
  currentSlide.value = currentSlide.value > 0 ? currentSlide.value - 1 : totalSlides - slidesPerView.value
}

function pause() { clearInterval(interval) }
function resume() { interval = setInterval(next, 5000) }

onMounted(() => {
  interval = setInterval(next, 5000)
  window.addEventListener('resize', () => {
    currentSlide.value = Math.min(currentSlide.value, totalSlides - slidesPerView.value)
  })
})

onUnmounted(() => {
  clearInterval(interval)
  window.removeEventListener('resize', () => {})
})
</script>

<style scoped>
.carousel-container {
  padding: 4rem 1rem;
  max-width: 1400px;
  margin: 0 auto;
}

.carousel-title {
  text-align: center;
  font-size: 1.75rem;
  font-weight: 600;
  color: #e2e8f0;
  margin-bottom: 2.5rem;
}

.carousel-wrapper {
  position: relative;
  display: flex;
  align-items: center;
}

.carousel-viewport {
  overflow: hidden;
  width: 100%;
}

.carousel-track {
  display: flex;
  transition: transform 0.7s ease;
  gap: 1.5rem;
}

.carousel-slide {
  flex: 0 0 calc(100% / v-bind(slidesPerView));
  display: flex;
  justify-content: center;
  align-items: center;
  /* Remove background/padding on mobile */
  background: transparent;
  padding: 0.5rem;
}

.carousel-image {
  width: 100%;
  max-height: 28rem;
  object-fit: contain;
  border-radius: 1.2rem;
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.35);
  transition: transform 0.3s ease;
  background: #0D1B2A; /* fallback if image fails */
}

/* Mobile: make image bigger, remove extra space */
@media (max-width: 640px) {
  .carousel-slide {
    padding: 0;
    /* Full height available */
  }

  .carousel-image {
    max-height: 70vh;           /* takes most of screen height */
    border-radius: 0.8rem;      /* slightly smaller radius on mobile */
    box-shadow: 0 10px 25px rgba(0,0,0,0.5);
  }

  .nav-btn {
    width: 3.5rem;
    height: 3.5rem;
    font-size: 1.8rem;
  }

  .prev { left: 0.5rem; }
  .next { right: 0.5rem; }
}

/* Hover effect (desktop only) */
@media (hover: hover) {
  .carousel-image:hover {
    transform: scale(1.03);
  }
}

/* NAV BUTTONS */
.nav-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(13, 27, 42, 0.85);
  border: 2px solid #FEA55F;
  color: #FEA55F;
  font-size: 2rem;
  width: 4rem;
  height: 4rem;
  border-radius: 50%;
  cursor: pointer;
  z-index: 10;
  transition: 0.3s;
}

.nav-btn:hover {
  background: #FEA55F;
  color: #011221;
}

.prev { left: -1rem; }
.next { right: -1rem; }
</style>
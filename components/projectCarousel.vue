<template>
  <div class="carousel-container">
    <h4 class="carousel-title" v-if="title">
      {{ title }}
    </h4>

    <div class="carousel-wrapper" @mouseenter="pause" @mouseleave="resume">
      <!-- Prev -->
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
            :style="{ flex: `0 0 ${100 / slidesPerView}%` }"
          >
            <img
              :src="getImageSrc(n)"
              :alt="`${projectName} visual ${n}`"
              class="carousel-image"
              loading="lazy"
            />
          </div>
        </div>
      </div>

      <!-- Next -->
      <button class="nav-btn next" @click="next">›</button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  projectName: { type: String, required: true },
  totalSlides: { type: Number, default: 10 },
  extension: { type: String, default: 'png' },
  title: { type: String, default: '' }
})

const currentSlide = ref(0)
const slidesPerView = ref(4)
let interval = null

function updateSlidesPerView() {
  const w = window.innerWidth

  if (w >= 1024) slidesPerView.value = 4
  else if (w >= 768) slidesPerView.value = 3
  else if (w >= 640) slidesPerView.value = 2
  else slidesPerView.value = 1

  const max = props.totalSlides - slidesPerView.value
  if (currentSlide.value > max) {
    currentSlide.value = Math.max(0, max)
  }
}

function getImageSrc(n) {
  return `/images/projects/${props.projectName}/a4-${n}.${props.extension}`
}

function next() {
  const max = props.totalSlides - slidesPerView.value
  currentSlide.value = currentSlide.value < max ? currentSlide.value + 1 : 0
}

function prev() {
  const max = props.totalSlides - slidesPerView.value
  currentSlide.value = currentSlide.value > 0 ? currentSlide.value - 1 : max
}

function pause() {
  clearInterval(interval)
}

function resume() {
  interval = setInterval(next, 5000)
}

onMounted(() => {
  updateSlidesPerView()
  window.addEventListener('resize', updateSlidesPerView)
  interval = setInterval(next, 5000)
})

onUnmounted(() => {
  clearInterval(interval)
  window.removeEventListener('resize', updateSlidesPerView)
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
}

/* Slides */
.carousel-slide {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Image only — no background boxes */
.carousel-image {
  width: 92%;
  aspect-ratio: 3 / 4;
  object-fit: cover;
  border-radius: 1.2rem;
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.35);
  transition: transform 0.3s ease;
  background: transparent;
}

/* Hover (desktop only) */
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

.prev {
  left: -1rem;
}

.next {
  right: -1rem;
}

/* Mobile adjustments */
@media (max-width: 640px) {
  .carousel-image {
    width: 95%;
  }

  .nav-btn {
    width: 3.5rem;
    height: 3.5rem;
    font-size: 1.8rem;
  }

  .prev { left: 0.5rem; }
  .next { right: 0.5rem; }
}
</style>

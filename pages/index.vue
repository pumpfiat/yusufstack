<template>
  <main v-if="!loading" id="hello">

    <!-- gradients -->
    <div class="css-blurry-gradient-blue"></div>
    <div class="css-blurry-gradient-green"></div>

    <section class="hero">
    
      <div class="head">
        <span>
          Hi all, I am
        </span>
        <h1>{{ config.name }}</h1>
        <span class="diple flex">
          >&nbsp;
		  <h2 class="typewriter">
  {{ roleText }}
</h2>

        </span>
      </div>

      <div id="info">
        <span class="action">
          // I build scalable web systems with clean architecture.
        </span>
        <span :class="{hide: isMobile}">
          // E-commerce, SaaS, productivity systems, automation.


        </span>
        <span :class="{hide: !isMobile}">
          // E-commerce, SaaS, productivity systems, automation.

        </span>
		<div class="cta-wrapper">
  <RouterLink to="/projects" class="project-btn">
    view-projects →
  </RouterLink>
</div>


      </div>
    </section>

    <!-- Snake Game (kept but hidden on mobile as before – we can personalize later) -->
    <section data-aos="fade-up" class="game" v-if="!isMobile">
      <SnakeGame />
    </section>

  </main>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import DevConfig from '~/developer.json'

const config = ref(DevConfig)

const isMobile = ref(false)
const loading = ref(false)

function handleResize() {
  if (process.client) {
    isMobile.value = window.innerWidth <= 1024
  }
}

/* ─────────────────────────────────────
   Clean Infinite Typewriter
───────────────────────────────────── */

const roles = [
  'Creative Director',
  'Official Notion Partner',
  'Product Builder',
  'Systems Designer',
  'Brand Launcher'
]

const roleText = ref('')
const roleIndex = ref(0)
const isDeleting = ref(false)

let timeout = null

function typeEffect() {
  const current = roles[roleIndex.value]

  if (!isDeleting.value) {
    roleText.value = current.substring(0, roleText.value.length + 1)

    if (roleText.value === current) {
      timeout = setTimeout(() => {
        isDeleting.value = true
        typeEffect()
      }, 1500)
      return
    }
  } else {
    roleText.value = current.substring(0, roleText.value.length - 1)

    if (roleText.value === '') {
      isDeleting.value = false
      roleIndex.value = (roleIndex.value + 1) % roles.length
    }
  }

  timeout = setTimeout(typeEffect, isDeleting.value ? 40 : 60)
}

onMounted(() => {
  handleResize()
  window.addEventListener('resize', handleResize)
  typeEffect()
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', handleResize)
  clearTimeout(timeout)
})
</script>


<style scoped>
/* ────────────────────────────────────────────────
   Your original styles – unchanged except minor cleanup
   ──────────────────────────────────────────────── */

#hello {
  display: flex;
  height: 100%;
  width: 100%;
  flex: 1 1 auto;
  padding-left: 275px;
  overflow: hidden;
}
/* ─────────────────────────────────────
   Premium Project Button
───────────────────────────────────── */

.cta-wrapper {
  margin-top: 2rem;
}

.project-btn {
  display: inline-flex;
  align-items: center;
  gap: 6px;

  padding: 12px 20px;

  font-family: 'Fira Code Retina';
  font-size: 14px;
  letter-spacing: 0.5px;

  color: #E5E9F0;
  text-decoration: none;

  border: 1px solid #1E2D3D;
  border-radius: 8px;

  background-color: #011221;

  transition: all 0.25s ease;
}

/* Hover */
.project-btn:hover {
  border-color: #43D9AD;
  color: #43D9AD;
  background-color: rgba(67, 217, 173, 0.05);
  transform: translateY(-2px);
}

/* Active */
.project-btn:active {
  transform: translateY(0px);
}


.hero {
  width: 100%;
  justify-content: center;
}

.game {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  justify-content: center;
  z-index: 20;
}

#hello .hero {
  display: flex;
  flex-direction: column;
  margin: 0rem;
}

#hello .head span {
  font-size: 18px;
  line-height: 1;
  color: #E5E9F0;
  font-family: 'Fira Code Retina';
}

#hello .head h1 {
  font-size: 58px;
  line-height: 1;
  color: #E5E9F0;
  font-family: 'Fira Code Regular';
  padding-top: 1rem;
  padding-bottom: 1rem;
}

#hello .head h2, #hello .head .diple {
  font-size: 32px;
  line-height: 1;
  color: #4D5BCE;
  font-family: 'Fira Code Retina';
}

.head {
  padding-bottom: 3rem;
}

#info {
  display: flex;
  flex-direction: column;
}

#info > span {
  font-size: 14px;
  line-height: 1;
  color: #8da9c6;
  font-family: 'Fira Code Retina';
  padding-bottom: 1rem;
}

.code {
  font-family: 'Fira Code Medium';
  color: #E5E9F0;
}

.code .identifier {
  color: #6172ff;
}

.code .variable-name {
  color: #43D9AD;
}

.code .operator {
  color: white;
}

.code .string {
  color: #E99287;
  text-decoration-line: underline;
  text-underline-offset: 4px;
}

#info {
  padding-block: 2.5rem;
}

#info .action {
  display: flex
}

.hide {
  display: none;
}

.css-blurry-gradient-blue {
  position: fixed;
  bottom: 25%;
  right: 5%;
  width: 300px;
  height: 300px;
  border-radius: 0% 0% 50% 50%;
  rotate: 10deg;
  filter: blur(70px);
  background: radial-gradient(circle at 50% 50%, rgba(77, 91, 206, 1), rgba(76, 0, 255, 0));
  opacity: 0.5;
  z-index: 10;
}

.css-blurry-gradient-green {
  position: absolute;
  top: 20%;
  right: 30%;
  width: 300px;
  height: 300px;
  border-radius: 0% 50% 0% 50%;
  filter: blur(70px);
  background: radial-gradient(circle at 50% 50%, rgba(67, 217, 173, 1), rgba(76, 0, 255, 0));
  opacity: 0.5;
  z-index: 10;
}

/* Typewriter Animation */
.typewriter {
  display: inline-block;
  position: relative;
}

.typewriter::after {
  content: '|';
  margin-left: 4px;
  animation: blink 1s infinite;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}


/* Mobile */
@media (max-width: 768px) {
  #hello {
    padding-left: 0;
  }

  #hello .hero {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin: 1.75rem;
  }

  .head {
    padding-top: 4rem;
  }

  #hello .head h2, #hello .head .diple {
    font-size: 20px;
    color: #43D9AD;
  }

  #info .action {
    display: none;
  }
}

/* Tablet */
@media (min-width: 768px) and (max-width: 1024px) {
  #hello {
    padding-left: 0;
  }
  #hello .hero {
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin: 1.75rem;
  }
  .head {
    padding-top: 4rem;
  }
}

/* Mid-large screens */
@media (min-width: 1024px) and (max-width: 1320px) {
  #hello {
    padding-left: 135px;
  }
}

/* LG */
@media (min-width: 1024px) {
  .css-blurry-gradient-blue {
    position: fixed;
    bottom: 10%;
    right: 10%;
    width: 500px;
    height: 500px;
    opacity: 0.7;
    border-radius: 100% 50% 100% 0%;
  }

  .css-blurry-gradient-green {
    position: fixed;
    top: 10%;
    right: 35%;
    filter: blur(100px);
    rotate: 10deg;
    width: 400px;
    height: 400px;
    opacity: 0.5;
    border-radius: 100% 0% 0% 0%;
    rotate: 20deg;
  }
}

/* Safari desktop: nudge game lower to match previous visual spacing */
@supports (-webkit-touch-callout: none) {
  @media (min-width: 1024px) {
    .game {
      transform: translateY(18px);
    }
  }
}

@media (min-width: 1920px) {
  #hello {
    padding-left: 310px;
  }
  #hello .head h1 {
    font-size: 62px;
  }
}

:global(html.is-safari) #hello {
  height: 100% !important;
  min-height: 0 !important;
  overflow: visible !important;
}
</style>
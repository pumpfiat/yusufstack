<template>
  <footer class="flex md:justify-between border-top text-menu-text font-fira_retina">

    <!-- LEFT: Social -->
    <div class="w-full flex justify-between md:justify-start">
      <span id="social-title" class="h-full flex justify-center items-center border-right px-5">
        find me in:
      </span>

      <div id="social-icons" class="flex">
        <NuxtLink
          :to="social.twitter.url + social.twitter.user"
          target="_blank"
          class="flex justify-center items-center"
        >
          <img src="/icons/social/linkedin.svg" alt="linkedin" />
        </NuxtLink>

        <NuxtLink
          :to="social.facebook.url + social.facebook.user"
          target="_blank"
          class="flex justify-center items-center"
        >
          <img src="/icons/social/googledrive.svg" alt="drive" />
        </NuxtLink>


      </div>
    </div>

    <!-- RIGHT: Brand Logos (Desktop Only) -->
    <div id="brand-logos" class="hidden md:flex items-center">

      <div class="brand"><img src="/brands/logo1.png" /></div>
      <div class="brand"><img src="/brands/logo2.svg" /></div>
      <div class="brand"><img src="/brands/logo3.png" /></div>
      <div class="brand"><img src="/brands/logo4.jpg" /></div>
      <div class="brand"><img src="/brands/logo5.png" /></div>
      <div class="brand"><img src="/brands/logo6.png" /></div>
      <div class="brand"><img src="/brands/logo7.png" /></div>
      <div class="brand"><img src="/brands/logo8.svg" /></div>

    </div>

  </footer>
</template>

<script setup>
import config from '~/developer.json'
const social = ref(config.contacts.social)
</script>

<script>
export default {
  name: 'AppFooter',
}
</script>

<style>

footer {
  height: 40px;
  min-height: 40px;
  font-size: 13px;
}

/* Hover effect */
footer a:hover {
  background-color: #1e2d3d74;
}

/* Social Icons */
#social-icons > a {
  border-right: 1px solid #1E2D3D;
  height: 100%;
  width: 50px;
}

#social-icons > a > img {
  width: 1.25rem;
  height: 1.25rem;
  margin: auto;
  opacity: 0.4;
}

/* Brand Logos Desktop */
#brand-logos {
  border-left: 1px solid #1E2D3D;
}

.brand {
  height: 100%;
  width: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-right: 1px solid #1E2D3D;
}

.brand img {
  max-height: 18px;
  max-width: 40px;
  opacity: 0.35;
  transition: opacity 0.2s ease;
}

.brand:hover img {
  opacity: 0.8;
}

/* Mobile adjustments */
@media (max-width: 768px) {

  #social-title {
    border-right: none;
  }

  #social-icons > a {
    border-right: none;
    border-left: 1px solid #1E2D3D;
  }

  #social-icons > a > img {
    width: 1.5rem;
    height: 1.5rem;
  }
}

</style>

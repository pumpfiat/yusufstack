<template>
<div class="bg-[#011221] text-white font-fira_regular">

    <!-- Top nav -->
    <div class="border-b border-[#1E2D3D] bg-[#0D1B2A] sticky top-0 z-10">
      <div class="max-w-7xl mx-auto px-6 py-4 flex items-center justify-between">
        <NuxtLink
          to="/projects"
          class="flex items-center gap-3 text-orange-400 hover:text-orange-300 transition-colors text-sm"
        >
          ← Back to Projects
        </NuxtLink>
        <div class="text-sm text-gray-500 hidden md:block">
          {{ project?.title || 'Project' }}
        </div>
      </div>
    </div>

    <!-- Hero -->
<!-- Hero -->
<div class="relative bg-[#011221]">

  <!-- Constrained container -->
  <div class="relative mx-auto max-w-[1600px]">

    <!-- Image -->
<img
  v-if="project?.img"
  :src="project.img"
  :alt="project.title"
class="
  w-full
  object-cover
  bg-[#011221]
  min-h-[520px]
  lg:min-h-[650px]
  xl:min-h-[720px]
  2xl:min-h-[760px]
  max-h-[900px]
"

/>



    <!-- Softer gradient -->
    <div class="
      absolute inset-0
      bg-gradient-to-t
      from-[#011221]/95
      via-[#011221]/30
      to-transparent
    "></div>

    <!-- Title Wrapper -->
    <div class="absolute inset-0 flex items-end">
      <div class="
        w-full
        max-w-7xl
        2xl:max-w-6xl
        mx-auto
        px-6
        2xl:px-0
        pb-10
        md:pb-16
        lg:pb-20
      ">
        <h1 class="
          text-3xl
          sm:text-4xl
          md:text-5xl
          lg:text-5xl
          xl:text-6xl
          2xl:text-6xl
          font-bold
          leading-tight
          xl:leading-[1.15]
          max-w-2xl
          md:max-w-3xl
          lg:max-w-4xl
          2xl:max-w-3xl
          drop-shadow-[0_6px_30px_rgba(0,0,0,0.7)]
        ">
          {{ project?.title || 'Project not found' }}
        </h1>
      </div>
    </div>

  </div>
</div>


    <!-- Main content -->
    <div class="max-w-5xl mx-auto px-6 py-12 lg:py-16">
<div v-if="project" class="prose prose-invert prose-lg max-w-none">

  <!-- Special Layout ONLY for Kajego -->
  <template v-if="slug === 'kaijego'">
    <div v-html="projectTop"></div>

    <KaijegoCarousel />

    <div v-html="projectBottom"></div>
  </template>

<template v-if="slug === 'uncover'">
  <div v-html="projectTop"></div>

<ProjectCarousel 
  project-name="uncover"
  :total-slides="11"
  extension="png"
  title="Uncover Skincare Visual Assets"
/>
  <div v-html="projectBottom"></div>
</template>

<template v-if="slug === 'sofit'">
  <div v-html="projectTop"></div>

<ProjectCarousel 
  project-name="sofit"
  :total-slides="14"
  extension="png"
  title="Sofit Training & Wellness Guides"
/>
  <div v-html="projectBottom"></div>
</template>

<template v-if="slug === 'chess-notion'">
  <div v-html="projectTop"></div>
  <div v-html="projectBottom"></div>
</template>

<template v-if="slug === 'maxx-improve-guides'">
  <div v-html="projectTop"></div>
  <ProjectCarousel 
  project-name="maxx-improve-guides"
  :total-slides="11"
  extension="png"
  title="Proffesional Guides for Ducth Audience"
/>
  <div v-html="projectBottom"></div>
</template>

<template v-if="slug === 'compasspdf'">
  <div v-html="projectContent"></div>
</template>


  <!-- Default Layout for ALL Other Projects -->
  <template v-else>
    <div v-html="projectContent"></div>
  </template>

  <!-- Tech tags (shared across all) -->


</div>


      <div v-else class="text-center py-24">
        <h2 class="text-3xl mb-4">Project not found</h2>
        <p class="text-gray-400 mb-8">The project you're looking for doesn't exist or has been moved.</p>
        <NuxtLink to="/projects" class="text-orange-400 hover:underline">
          ← Return to all projects
        </NuxtLink>
      </div>
    </div>

    
  </div>
</template>

<script setup>
import DevConfig from '~/developer.json'
import KaijegoCarousel from '~/components/KaijegoCarousel.vue'


const route = useRoute()
const slug = route.params.slug

const project = Object.values(DevConfig.projects || {}).find(p => {
  const urlSlug = p.url?.split('/').pop() || ''
  return urlSlug === slug
})

const projectContent = ref('')
const projectTop = ref('')
const projectBottom = ref('')


onMounted(() => {
  if (!project) return
  
if (slug === 'kaijego') {

projectTop.value = `
  <h2 class="text-3xl md:text-4xl font-bold mt-2 mb-10 text-orange-400">
    No limits except the ones we create for ourselves.
  </h2>

  <div class="grid md:grid-cols-2 gap-10 mb-14 text-gray-300">
    <div>
      <h3 class="text-xl font-semibold mb-4 text-white">Key Facts</h3>
      <ul class="space-y-2">
        <li><strong>Period:</strong> 2022–2024</li>
        <li><strong>Position:</strong> Designer – Branding, Digital and Print</li>
        <li><strong>Brand:</strong> Kajego</li>
        <li><strong>Impact:</strong> Empowered lower-ranked passport owners</li>
      </ul>
    </div>
    <div>
      <p class="italic text-gray-400">
        A visual journey chronicling Alma Asinobi — the fastest woman to visit 7 continents with a lower-ranked passport.
      </p>
    </div>
  </div>

  <h3 class="text-2xl font-semibold mt-14 mb-5">Company</h3>
  <p class="mb-7 leading-relaxed">
    Kajego is a travel empowerment platform founded by Alma Asinobi, dedicated to helping individuals with lower-ranked passports navigate the world with confidence. More than a travel service, Kajego represents a movement — breaking down invisible barriers, complex immigration rules, and social limitations. Through travel education, curated resources, and storytelling, Kajego proves dreams are possible, regardless of where your passport was issued.
  </p>

  <h3 class="text-2xl font-semibold mt-14 mb-5">Challenge</h3>
  <p class="mb-7 leading-relaxed">
    For many people holding lower-ranked passports, international travel often feels like an unattainable dream. The complexities of visa applications, travel restrictions, and financial limitations create a sense of impossibility. Alma Asinobi, the founder, envisioned a way to show that global adventures are within reach — but it needed a creative core to inspire the audience while reflecting the brand’s message of boundless possibility.
  </p>

  <h3 class="text-2xl font-semibold mt-14 mb-6">Details</h3>
  <p class="mb-12 leading-relaxed">
    This project documents Alma Asinobi’s historic journey across all 7 continents, transforming limitation into liberation. The design system celebrates momentum, resilience, and global ambition — inviting others to step beyond borders and redefine what’s possible.
  </p>

  <!-- Large Featured Image -->
  <div class="mt-16">
    <img 
      src="/images/projects/kaijego/hero-large.png"
      alt="Alma Asinobi global journey"
      class="w-full rounded-2xl shadow-2xl object-cover"
    />
    <p class="text-center text-gray-400 italic mt-6 text-lg">
      A visual journey chronicling Alma Asinobi — the fastest woman to visit 7 continents with a lower-ranked passport.
    </p>
  </div>
`


  projectBottom.value = `
    <h3 class="text-2xl font-semibold mt-16 mb-5">Opportunity</h3>
    <p class="mb-7 leading-relaxed">
      In collaboration with Kajego, I designed "Around the World with Alma Asinobi" — a visual storytelling concept centered on Alma’s own travel experiences. This design was more than a graphic; it was a narrative-driven piece that illustrated how someone with a lower-ranked passport could journey across the globe, overcoming obstacles. The visual project emphasized:
    </p>

    <ol class="list-decimal pl-6 space-y-3 mb-8 text-gray-300">
      <li>Dynamic, uplifting travel milestones as a symbol of what’s possible.</li>
      <li>Alma’s personal narrative aesthetic that reflected freedom, cultural richness, and movement.</li>
      <li>Empowerment messaging aligned with Kajego’s mission of breaking limitations.</li>
    </ol>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Impact</h3>
    <p class="mb-7 leading-relaxed">
      The "Around the World with Alma Asinobi" project resonated strongly within Kajego’s community. It became a storytelling centerpiece that increased engagement and inspired followers by turning Alma’s journey into a relatable, aspirational example. The campaign reinforced Kajego’s identity as a brand that champions limitless ambition — not just for the privileged, but for underrepresented travelers. It laid the groundwork for future brand storytelling initiatives aimed at shifting perceptions and empowering a new generation of global citizens.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Testimonial</h3>
    <blockquote class="border-l-4 border-orange-500 pl-6 py-2 my-10 italic text-lg text-gray-300">
      "Working with Yusuf on the 'Around the World with Alma Asinobi' project was one of the most intuitive creative experiences I've had. His ability to translate the emotional core of my message — breaking free from passport limitations — into a visual narrative was truly moving. The final design felt free from dreamlike; it captured the essence of Kajego in a way that still amazes me. Yusuf’s calm, thoughtful approach throughout the process made collaboration seamless. His work gave me the story I’ve always wanted to tell."
      <footer class="mt-6 text-base not-italic text-gray-400">
        — Alma Asinobi, Founder Kajego.com
      </footer>
    </blockquote>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Core Skills</h3>
    <div class="flex flex-wrap gap-3 mb-12">
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Visual Storytelling</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Art Direction</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Innovation</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Digital Transformation</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Web-Special</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">E-Commerce</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Corporate Identity</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Corporate Design</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Adobe Suites</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Canva</span>
    </div>
  `
}
else if (slug === 'uncover') {
  projectTop.value = `
    <h2 class="text-3xl md:text-4xl font-bold mt-2 mb-10 text-orange-400">
      Beauty isn't a standard — it's a story in every shade.
    </h2>

    <div class="grid md:grid-cols-2 gap-10 mb-14 text-gray-300">
      <div>
        <h3 class="text-xl font-semibold mb-4 text-white">Key Facts</h3>
        <ul class="space-y-2">
          <li><strong>Period:</strong> 2023–2025</li>
          <li><strong>Position:</strong> Brand Designer</li>
          <li><strong>Brand:</strong> Uncover</li>
          <li><strong>Impact:</strong> Launch across Africa (digital + print)</li>
        </ul>
      </div>
      <div>
        <p class="italic text-gray-400">
          A collection of digital and print designs created for Uncover Skincare as they expanded across African markets.
        </p>
      </div>
    </div>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Company</h3>
    <p class="mb-7 leading-relaxed">
      Uncover Skincare is a pioneering beauty and wellness brand, designed specifically for African skin. Founded by women, for women, Uncover is on a mission to transform skincare across the continent by combining science-backed formulations with culturally relevant communication. The brand is built on the belief that skincare is not just about appearance, but about confidence, empowerment, and self-care tailored to the unique needs of African skin.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Challenge</h3>
    <p class="mb-7 leading-relaxed">
      As Uncover Skincare began entering new African countries, the brand needed a fresh, visually appealing way to introduce its products and philosophy to unfamiliar markets. The key challenge was to maintain Uncover’s premium, contemporary identity while adapting its communication to different cultures and audiences — both online and offline.
    </p>
    <p class="mb-7 leading-relaxed">
      They required elegant, informative print materials to accompany product launches in new countries. Cohesive digital design assets that reflected the brand’s identity while welcoming a new audience. A scalable, repeatable system to use as the brand entered more markets.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Details</h3>
    <p class="mb-8 leading-relaxed">
      A collection of digital and print designs I created for Uncover Skincare as they expanded across African markets. These materials reflect Uncover’s science-backed, melanin-friendly products, blending clean design with culturally relevant storytelling for both retail and digital platforms.
    </p>

    <!-- Large Featured Image + Caption at the end of top part -->
    <div class="mt-16 mb-20">
      <img 
        src="/images/projects/uncover/hero-large.png"
        alt="Uncover Skincare campaign visuals"
        class="w-full rounded-2xl shadow-2xl object-cover"
      />
      <p class="text-center text-gray-400 italic mt-6 text-lg">
        A collection of digital and print designs I created for Uncover Skincare as they expanded across African markets. These visuals reflect Uncover’s science-backed, melanin-friendly products, blending clean design with culturally relevant storytelling for both retail and digital platforms.
      </p>
    </div>
  `

  projectBottom.value = `
    <h3 class="text-2xl font-semibold mt-16 mb-5">Opportunity</h3>
    <p class="mb-7 leading-relaxed">
      I collaborated with Uncover to design a suite of digital and print materials that would accompany the brand’s entrance into new African markets. These included:
    </p>
    <ol class="list-decimal pl-6 space-y-3 mb-8 text-gray-300">
      <li>Elegant product flyers and shelf talkers for retail spaces</li>
      <li>Location-specific campaign visuals adapted to local aesthetics</li>
      <li>Digital launch creatives for ads, social content, and e-commerce presence</li>
    </ol>
    <p class="mb-7 leading-relaxed">
      The designs reflected Uncover’s science-meets-core identity: clean, feminine, modern — and were crafted to help customers quickly understand and trust the benefits of Uncover’s offerings.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Impact</h3>
    <p class="mb-7 leading-relaxed">
      The visual materials played a pivotal role in Uncover’s market launches across Africa. They helped create brand consistency across borders, increased product recognition, and supported local retail partnerships by offering professionally designed print collaterals.
    </p>
    <p class="mb-7 leading-relaxed">
      As a result, Uncover maintained a polished, premium appearance in every market they entered, reinforcing trust and credibility with new customers. The design indirectly contributed to a successful rollout strategy and supported Uncover’s mission of redefining beauty for African women, one country at a time.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Testimonial</h3>
    <blockquote class="border-l-4 border-orange-500 pl-6 py-2 my-10 italic text-lg text-gray-300">
      "Yusuf came into our brand at a pivotal time — right as we were expanding from Kenya into West Africa. His design work for our product materials helped us communicate skincare across cultural lines, helping us create tools that connected with new customers while staying true to our values. Beyond the visuals, Yusuf provided crucial strategic advice that made our entry into new markets feel less overwhelming. We couldn’t have asked for better support."
      <footer class="mt-6 text-base not-italic text-gray-400">
        — Sneha Mehta, Founder Uncover
      </footer>
    </blockquote>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Core Skills</h3>
    <div class="flex flex-wrap gap-3 mb-12">
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Visual Storytelling</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Art Direction</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Innovation</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Country-Specific Strategy</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Print Design</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">E-Commerce</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Corporate Identity</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Diversity & Inclusion</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Adobe Suites</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Canva</span>
    </div>
  `
}
else if (slug === 'sofit') {
  projectTop.value = `
    <h2 class="text-3xl md:text-4xl font-bold mt-2 mb-10 text-orange-400">
      Investment in wellness is never a waste.
    </h2>

    <div class="grid md:grid-cols-2 gap-10 mb-14 text-gray-300">
      <div>
        <h3 class="text-xl font-semibold mb-4 text-white">Key Facts</h3>
        <ul class="space-y-2">
          <li><strong>Period:</strong> 2024</li>
          <li><strong>Position:</strong> Freelance Designer</li>
          <li><strong>Brand:</strong> Sofit</li>
          <li><strong>Impact:</strong> Downloaded by more than 24000 fans</li>
        </ul>
      </div>
      <div>
        <p class="italic text-gray-400">
          Digital and print products including workout guides, recipe books, and training schedules for a growing African fitness community.
        </p>
      </div>
    </div>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Company</h3>
    <p class="mb-7 leading-relaxed">
      Sofit NGR is one of Nigeria's biggest fitness and wellness YouTube influencers, founded by Sandra Okeke. Known for her engaging home workout routines, healthy recipe content, and motivational lifestyle advice, she has built a passionate online community committed to fitness, self-care, and healthy living. Beyond YouTube, Sofit has expanded her influence through digital products, including workout guides, cookbooks, and resources designed specifically for local realities and African lifestyles.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Challenge</h3>
    <p class="mb-7 leading-relaxed">
      As Sofit's digital following grew rapidly, the need arose to translate her video-based content into structured, user-friendly, and visually appealing digital products. The challenge was to create professional, on-brand training guides and cookbooks that matched her vibrant personality and connected deeply with her target audience — while maintaining clarity, ease of use, and motivation for her followers.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Details</h3>
    <p class="mb-8 leading-relaxed">
      Bringing Fitness to Life — a look inside the digital training guide I designed for Sofit NGR. Clean design, clear layouts, bold and motivating content crafted to inspire and empower a growing Nigerian fitness community.
    </p>

    <!-- Large Featured Image + Caption at the end of top part -->
    <div class="mt-16 mb-20">
      <img 
        src="/images/projects/sofit/hero-large.png"
        alt="Sofit training guide spread"
        class="w-full rounded-2xl shadow-2xl object-cover"
      />
      <p class="text-center text-gray-400 italic mt-6 text-lg">
        Bringing Fitness to Life — A look inside the digital training guide I designed for Sofit NGR. Clean layouts, bold visuals, and motivating content crafted to inspire and empower a growing African fitness community.
      </p>
    </div>
  `

  projectBottom.value = `
    <h3 class="text-2xl font-semibold mt-16 mb-5">Opportunity</h3>
    <p class="mb-7 leading-relaxed">
      Working closely with Sofit, I developed custom-designed digital products that brought her brand to life beyond the screen. These included workout guides, recipe books, and training schedules, crafted with African audiences in mind.
    </p>
    <p class="mb-7 leading-relaxed">
      Visually appealing layouts featuring exercise breakdowns, healthy recipe ideas, and motivational content were created to inspire and empower followers. Consistent brand-aligned visual elements, color schemes, and typography reinforced Sofit’s energetic, approachable identity across all materials.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Impact</h3>
    <p class="mb-7 leading-relaxed">
      The release of these digital products elevated Sofit’s brand perception, offering followers something tangible, practical, and motivational. The training guides and cookbooks were met with positive feedback from the community, helping strengthen her personal brand, open new revenue opportunities through digital sales, and provide lasting resources for a growing fitness community in Nigeria and the diaspora.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Testimonial</h3>
    <blockquote class="border-l-4 border-orange-500 pl-6 py-2 my-10 italic text-lg text-gray-300">
      "Running a brand while creating content full-time can be overwhelming, but Yusuf made things follow so much easier for me. He created a digital guide that completely captured the feel of my brand — clean, motivating, and accessible. Whether it was designing workout pages or formatting my cookbooks, his attention to detail and ability to translate my vision into easy-to-use products was unmatched. I trusted him immediately, and the result was exactly what I wanted to serve."
      <footer class="mt-6 text-base not-italic text-gray-400">
        — Sandra Okeke, YouTuber & Founder Sofit
      </footer>
    </blockquote>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Core Skills</h3>
    <div class="flex flex-wrap gap-3 mb-12">
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Visual Storytelling</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Art Direction</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Scheduling</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Innovation</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Market Research</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Pre-Launch</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">E-Commerce</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Casual Branding</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Premium Design</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Adobe Suites</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Canva</span>
    </div>
  `
}
else if (slug === 'chess-notion') {
  projectTop.value = `
    <h2 class="text-3xl md:text-4xl font-bold mt-2 mb-10 text-orange-400">
      The smartest players don't just play — they study.
    </h2>

    <div class="grid md:grid-cols-2 gap-10 mb-14 text-gray-300">
      <div>
        <h3 class="text-xl font-semibold mb-4 text-white">Key Facts</h3>
        <ul class="space-y-2">
          <li><strong>Position:</strong> No-Code Expert</li>
          <li><strong>Platform:</strong> Notion</li>
          <li><strong>Period:</strong> 2023 – Present</li>
          <li><strong>Impact:</strong> Helped more than 10,000 people learn chess</li>
          <li><strong>Solution:</strong> Notion + Zapier automation</li>
        </ul>
      </div>
      <div>
        <p class="italic text-gray-400">
          Chess Notion templates: physical notebooks replaced with powerful, flexible, digital workspaces for serious players and coaches.
        </p>
      </div>
    </div>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Company</h3>
    <p class="mb-7 leading-relaxed">
      Chess Notion is a niche digital brand that creates beautifully structured Notion templates tailored for chess players, enthusiasts, and coaches. From training trackers and opening repertoires to post-game analysis workspaces, Chess Notion merges the timeless game of strategy with the modern flexibility of no-code tools. The brand offers a mix of free and premium templates, giving the global chess community powerful, easy-to-use digital tools to study, track, and improve.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Challenge</h3>
    <p class="mb-7 leading-relaxed">
      When I joined the project, the challenge was clear: chess players often rely on scattered tools — physical notebooks, clunky spreadsheets, third-party apps — for studying games, tracking performance, and analyzing openings. There was no simple, all-in-one chess hub that allowed players and coaches to organize their chess life in a seamless, flexible way.
    </p>
    <p class="mb-7 leading-relaxed">
      We needed to position Notion as that solution and design templates that would feel natural for chess minds while unlocking the powerful organizational features of no-code tools.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Details</h3>
    <p class="mb-8 leading-relaxed">
      A glimpse into the custom Chess Notion templates I created — from game breakdown dashboards to Chess 101 starter kits and post-game analysis logs. Designed for players and coaches who want to track, learn, and improve — all inside their Notion workspace.
    </p>

    <!-- Large Featured Image + Caption at the end of top part -->
    <div class="mt-16 mb-20">
      <img 
        src="/images/projects/chess-notion/hero-large.png"
        alt="Chess Notion workspace overview"
        class="w-full rounded-2xl shadow-2xl object-cover"
      />
      <p class="text-center text-gray-400 italic mt-6 text-lg">
        A glimpse into the custom Chess Notion templates I created — from game breakdown dashboards to Chess 101 starter kits and post-game analysis logs. Designed for players and coaches who want to track, learn, and improve — all inside their Notion workspace.
      </p>
    </div>
  `

  projectBottom.value = `
    <h3 class="text-2xl font-semibold mt-16 mb-5">Opportunity</h3>
    <p class="mb-7 leading-relaxed">
      As a Notion expert and believer in the power of no-code solutions, I saw an opportunity to transform how chess players manage their training and growth. I use Notion a lot for program management, and it's a tool I enjoy using a lot.
    </p>
    <p class="mb-7 leading-relaxed">
      We developed a series of modular, user-friendly templates:
    </p>
    <ul class="list-disc pl-6 space-y-2 mb-8 text-gray-300">
      <li>Training Planners</li>
      <li>Opening Repertoire Libraries</li>
      <li>Post-Game Analysis Logs</li>
      <li>Performance Trackers</li>
      <li>Chess Video/Book/Databases</li>
    </ul>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Impact</h3>
    <p class="mb-7 leading-relaxed">
      The templates quickly gained traction within the chess community, offering both free resources and premium tools for serious players and coaches. Coaches could now track players had a clear, motivating structure for personal growth.
    </p>
    <p class="mb-7 leading-relaxed">
      Beyond Chess Notion, this project also became a proof point for how no-code tools like Notion can solve real, everyday problems in niche communities — something I continue to advocate for in my work.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Core Skills</h3>
    <div class="flex flex-wrap gap-3 mb-12">
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">No-Code Solution</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Art Direction</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Automation</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Digital Transformation</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Data Base</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">E-Commerce</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Corporate Identity</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Notion</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Zapier</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Corporate Design</span>
    </div>
  `
}
else if (slug === 'maxx-improve-guides') {
  projectTop.value = `
    <h2 class="text-3xl md:text-4xl font-bold mt-2 mb-10 text-orange-400">
      Power isn't just what you have — it's how you use it.
    </h2>

    <div class="grid md:grid-cols-2 gap-10 mb-14 text-gray-300">
      <div>
        <h3 class="text-xl font-semibold mb-4 text-white">Key Facts</h3>
        <ul class="space-y-2">
          <li><strong>Position:</strong> Creative Director</li>
          <li><strong>Period:</strong> 2023 – Present</li>
          <li><strong>Branding:</strong> Instructional Material</li>
          <li><strong>Market:</strong> Successful launch across Europe and America</li>
          <li><strong>Products:</strong> 14+ enhancement guides</li>
        </ul>
      </div>
      <div>
        <p class="italic text-gray-400">
          Comprehensive, user-friendly instructional guides (digital + print) that educate and empower customers safely and effectively.
        </p>
      </div>
    </div>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Company</h3>
    <p class="mb-7 leading-relaxed">
      Maxx Improve is a Shopify-based eCommerce brand specializing in male enhancement products. The brand focuses on performance, overall wellbeing, and helping men improve confidence through science-backed, high-quality formulations. Maxx operates predominantly online and ships worldwide, prioritizing discretion, quality, and customer education to ensure safe, effective product use.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Challenge</h3>
    <p class="mb-7 leading-relaxed">
      When I joined the Maxx Improve project, one of the major gaps was the lack of clear, approachable instructional content for customers. Many buyers were new to enhancement products and felt uncertain about how to properly use them, what to expect, and how to safely integrate them into their routine. The existing content was often overly clinical, vague, or difficult to access — leading to customer confusion, potential misuse, and missed opportunities to build trust and loyalty.
    </p>
    <p class="mb-7 leading-relaxed">
      The challenge was to develop comprehensive, user-friendly instructional guides that could be delivered in both print (included with physical packages) and digital formats (downloadable after purchase), helping customers get the most out of their purchases while reinforcing the brand’s professional, supportive image.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Details</h3>
    <p class="mb-8 leading-relaxed">
      A clean, structured collection of instructional guides created for Maxx Improve — designed to educate customers on proper product use, dosage, safety guidelines, and expected results. These guides ensure customers receive clear, professional, easy-to-follow directions — whether unboxing their package or downloading digital resources online.
    </p>

    <!-- Large Featured Image + Caption at the end of top part -->
    <div class="mt-16 mb-20">
      <img 
        src="/images/projects/maxx-improve-guides/hero-large.png"
        alt="Maxx Improve instructional guides"
        class="w-full rounded-2xl shadow-2xl object-cover"
      />
      <p class="text-center text-gray-400 italic mt-6 text-lg">
        A clean, structured collection of instructional guides created for Maxx Improve — designed for both print and digital use. These guides ensure customers receive clear, professional, and easy-to-follow directions, whether unboxing their package or downloading resources online.
      </p>
    </div>
  `

  projectBottom.value = `
    <h3 class="text-2xl font-semibold mt-16 mb-5">Opportunity</h3>
    <p class="mb-7 leading-relaxed">
      This project was an opportunity to turn a simple purchase into a complete product experience. By crafting well-designed, accessible guides, we could help Maxx Improve stand out in a competitive, often poorly-served niche.
    </p>
    <p class="mb-7 leading-relaxed">
      I worked closely with the brand team to develop a series of instructional materials that would serve two key functions:
    </p>
    <ul class="list-disc pl-6 space-y-2 mb-8 text-gray-300">
      <li>Educate customers on proper product use, dosage, safety guidelines, and expected results</li>
      <li>Enhance the unboxing relationship and digital follow-up experience, turning a transactional interaction into an informative one</li>
    </ul>
    <p class="mb-7 leading-relaxed">
      Printed guides were professionally designed and included in the package; digital guides were downloadable, with additional details, tips, and Q&A sections. This allowed us to tailor content depending on product type — from performance supplements to topical solutions.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Impact</h3>
    <p class="mb-7 leading-relaxed">
      The introduction of these instructional materials created an immediate, positive shift in customer satisfaction and product confidence:
    </p>
    <ul class="list-disc pl-6 space-y-2 mb-8 text-gray-300">
      <li>Increased clarity and ease of use: Customers felt equipped to safely use the products, reducing support queries and confusion</li>
      <li>Improved product experience: The attractive, well-written guides added a premium feel to the customer journey — particularly the printed versions included in every order</li>
      <li>Strengthened brand trust and loyalty: By proactively educating customers and offering ongoing support, Maxx Improve positioned itself as a supportive, credible leader in the male wellness space</li>
      <li>Enhanced retention and repeat sales: Better product understanding translated to immediately better results for customers, which in turn drove repeat purchases and positive word-of-mouth</li>
    </ul>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Testimonial</h3>
    <blockquote class="border-l-4 border-orange-500 pl-6 py-2 my-10 italic text-lg text-gray-300">
      "I've worked with creatives in different countries, but Yusuf stood out. After some rough experiences with freelancers in Nigeria, I honestly didn't expect the level of quality he delivered. He handled everything from product instructionals to print guides — with a level of detail that matched agencies in the €50,000 European range. Not only was the design beautiful and easy to follow, but his calm tone instinctively aligned with our brand. The project was smooth, the results were better than expected, and I know I'll be working with him again."
      <footer class="mt-6 text-base not-italic text-gray-400">
        — Robin Osterbosch, Founder Maxximprove.com
      </footer>
    </blockquote>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Core Skills</h3>
    <div class="flex flex-wrap gap-3 mb-12">
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Info Product Design</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Art Direction</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Branding</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Print Design</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">E-Commerce</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Instructional Design</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Corporate Identity</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Corporate Design</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Adobe Suites</span>
    </div>
  `
}
else if (slug === 'notion') {
  projectContent.value = `
    <h2 class="text-3xl md:text-4xl font-bold mt-2 mb-10 text-orange-400">
      Notion: Build, Scale, Automate.
    </h2>

    <div class="grid md:grid-cols-2 gap-10 mb-14 text-gray-300">
      <div>
        <h3 class="text-xl font-semibold mb-4 text-white">Key Facts</h3>
        <ul class="space-y-2">
          <li><strong>Role:</strong> Official Notion Partner & Community Ambassador</li>
          <li><strong>Period:</strong> 2022 – Present</li>
          <li><strong>Impact:</strong> Built custom Notion systems for 100+ businesses, teams, startups & NGOs</li>
          <li><strong>Focus:</strong> No-code operations, knowledge systems, automation & scalable workflows</li>
        </ul>
      </div>
      <div>
        <p class="italic text-gray-400">
          Helping organizations design human-friendly, long-term scalable systems using Notion as the central nervous system.
        </p>
      </div>
    </div>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Role & Contribution</h3>
    <p class="mb-7 leading-relaxed">
      As an official Notion Partner and active member of the Notion community, I help organizations — from early-stage startups to growing NGOs and creator teams — design and implement powerful, human-friendly systems that support clarity, collaboration, and long-term growth.
    </p>
    <p class="mb-7 leading-relaxed">
      Over the years I have built and delivered more than 100 custom Notion workspaces, templates, operating systems, and automation flows — helping teams centralize knowledge, reduce friction, improve decision-making, and scale without unnecessary complexity.
    </p>

    <p class="mb-8 leading-relaxed">
      Beyond building systems, I have delivered talks and workshops across West Africa and the Atlantic region, led internal ambassador projects, reported bugs directly to the Notion team, and onboarded a large number of businesses into effective Notion usage.
    </p>

    <!-- Hero image after intro/key facts -->


    <!-- Business Operations -->
    <h3 class="text-2xl font-semibold mt-20 mb-6 text-white">Business Operations</h3>
    <p class="mb-8 leading-relaxed text-gray-300">
      Templates used by agencies, founders, and growing teams after juggling dozens of tools in their backend. From onboarding clients to internal SOPs, a set of scalable systems for SOPs, meetings, workflows, and more.
    </p>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mb-16">
      <img src="/images/projects/notion/business-1.png" alt="Client Onboarding HQ" class="w-full rounded-lg border border-[#1E2D3D]">
      <img src="/images/projects/notion/business-2.png" alt="SOP & Wiki Manager" class="w-full rounded-lg border border-[#1E2D3D]">
      <img src="/images/projects/notion/business-3.png" alt="Admin Hub" class="w-full rounded-lg border border-[#1E2D3D]">
      <!-- add more if you have them -->
    </div>

    <!-- Hero image after Business Operations -->
    <div class="mt-16 mb-20">
      <img 
        src="/images/projects/notion/business-hero.png"
        alt="Business operations dashboard"
        class="w-full rounded-2xl shadow-2xl object-cover"
      />
      <p class="text-center text-gray-400 italic mt-6 text-lg">
        Templates used by agencies, founders, and growing teams to centralize SOPs, meetings, client onboarding, admin hubs, and more — all inside Notion.
      </p>
    </div>

    <!-- Project Management -->
    <h3 class="text-2xl font-semibold mt-20 mb-6 text-white">Project Management</h3>
    <p class="mb-8 leading-relaxed text-gray-300">
      Full project trackers, launch boards, content calendars — all centralized in Notion so nothing falls through the cracks.
    </p>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mb-16">
      <img src="/images/projects/notion/project-1.png" alt="Client Project Tracker" class="w-full rounded-lg border border-[#1E2D3D]">
      <img src="/images/projects/notion/project-2.png" alt="Product Launch Board" class="w-full rounded-lg border border-[#1E2D3D]">
      <img src="/images/projects/notion/project-3.png" alt="Content Calendar" class="w-full rounded-lg border border-[#1E2D3D]">
      <!-- add more if you have them -->
    </div>

    <!-- Hero image after Project Management -->
    <div class="mt-16 mb-20">
      <img 
        src="/images/projects/notion/project-hero.png"
        alt="Project management hub"
        class="w-full rounded-2xl shadow-2xl object-cover"
      />
      <p class="text-center text-gray-400 italic mt-6 text-lg">
        Full project trackers, launch boards, content calendars — everything centralized so nothing falls through the cracks.
      </p>
    </div>

    <!-- CRM & People Systems -->
    <h3 class="text-2xl font-semibold mt-20 mb-6 text-white">CRM & People Systems</h3>
    <p class="mb-8 leading-relaxed text-gray-300">
      Lightweight CRM, client management, onboarding flows, and HR trackers — all living inside Notion.
    </p>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mb-16">
      <img src="/images/projects/notion/crm-1.png" alt="Sales CRM" class="w-full rounded-lg border border-[#1E2D3D]">
      <img src="/images/projects/notion/crm-2.png" alt="HR / Onboarding System" class="w-full rounded-lg border border-[#1E2D3D]">
      <img src="/images/projects/notion/crm-3.png" alt="Client Manager" class="w-full rounded-lg border border-[#1E2D3D]">
      <!-- add more if you have them -->
    </div>

    <!-- Hero image after CRM & People Systems -->
    <div class="mt-16 mb-20">
      <img 
        src="/images/projects/notion/crm-hero.png"
        alt="CRM and people systems"
        class="w-full rounded-2xl shadow-2xl object-cover"
      />
      <p class="text-center text-gray-400 italic mt-6 text-lg">
        Lightweight CRM, client management, onboarding flows, and HR trackers — all living inside Notion.
      </p>
    </div>

    <!-- Personal Use -->
    <h3 class="text-2xl font-semibold mt-20 mb-6 text-white">Personal Use</h3>
    <p class="mb-8 leading-relaxed text-gray-300">
      Life OS, habit trackers, finance dashboards, second brain — systems I use daily to stay organized and intentional.
    </p>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mb-16">
      <img src="/images/projects/notion/personal-1.png" alt="Life OS Dashboard" class="w-full rounded-lg border border-[#1E2D3D]">
      <img src="/images/projects/notion/personal-2.png" alt="Habit & Finance Tracker" class="w-full rounded-lg border border-[#1E2D3D]">
      <img src="/images/projects/notion/personal-3.png" alt="Personal Finance OS" class="w-full rounded-lg border border-[#1E2D3D]">
      <!-- add more if you have them -->
    </div>

    <!-- Hero image after Personal Use -->
    <div class="mt-16 mb-20">
      <img 
        src="/images/projects/notion/personal-hero.png"
        alt="Personal use dashboards"
        class="w-full rounded-2xl shadow-2xl object-cover"
      />
      <p class="text-center text-gray-400 italic mt-6 text-lg">
        Life OS, habit trackers, finance dashboards, second brain — systems I use daily to stay organized and intentional.
      </p>
    </div>

    <!-- Core Skills -->
    <h3 class="text-2xl font-semibold mt-20 mb-6">Core Skills</h3>
    <div class="flex flex-wrap gap-3 mb-12">
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Notion Systems</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">No-Code Architecture</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Workflow Automation</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Zapier Integration</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Operating Systems Design</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Knowledge Management</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Team Enablement</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Community Building</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Notion Partner</span>
    </div>
  `
}
else if (slug === 'osofnotion') {
  projectContent.value = `
    <h2 class="text-3xl md:text-4xl font-bold mt-2 mb-10 text-orange-400">
      Premium Notion systems — built to help creators run better businesses.
    </h2>

    <div class="grid md:grid-cols-2 gap-10 mb-14 text-gray-300">
      <div>
        <h3 class="text-xl font-semibold mb-4 text-white">Key Facts</h3>
        <ul class="space-y-2">
          <li><strong>Role:</strong> Creative Director, Template Designer & Full Store Builder</li>
          <li><strong>Platform:</strong> Gumroad + Notion</li>
          <li><strong>Period:</strong> 2023 – Present</li>
          <li><strong>Impact:</strong> Premium Notion templates & PDF guides sold to hundreds of creators & businesses</li>
          <li><strong>Website:</strong> <a href="https://osofnotion.gumroad.com/" target="_blank" class="text-orange-400 hover:underline">osofnotion.com</a></li>

        </ul>
      </div>
      <div>
        <p class="italic text-gray-400">
          Built the entire Gumroad-powered ecommerce store, designed all premium templates, created downloadable PDF guides, and established a system for delivering custom Notion solutions to clients.
        </p>
      </div>
    </div>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Company</h3>
    <p class="mb-7 leading-relaxed">
      Osof Notion is a premium Notion template brand helping creators, solopreneurs, and small businesses build better operations, track progress, manage finances, and scale without chaos. The store offers high-quality, ready-to-use Notion systems alongside detailed PDF guides and a custom build service for clients who need tailored solutions.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Challenge</h3>
    <p class="mb-7 leading-relaxed">
      The goal was to create a professional, trustworthy online presence that could sell premium Notion products at scale. Most creators struggle to package their knowledge into clean, valuable digital products — and even fewer succeed at building a beautiful, high-converting store that feels premium and credible.
    </p>
    <p class="mb-7 leading-relaxed">
      We needed a complete system: beautiful templates that solve real problems, clear PDF companions for offline use, a polished Gumroad storefront, pricing strategy, product imagery, and a process for delivering custom client work — all while maintaining a strong, consistent brand identity.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Details</h3>
    <p class="mb-8 leading-relaxed">
      I built the entire ecommerce experience from ideation to launch: designed every premium template, created companion PDF guides, crafted product visuals, built the Gumroad storefront, set up pricing & checkout flow, and established a custom build pipeline for high-ticket clients.
    </p>

    <!-- Hero image + improved caption -->
    <div class="mt-16 mb-20">
      <img 
        src="/images/projects/osof-notion/hero-main.png"
        alt="Osof Notion premium templates and brand assets"
        class="w-full rounded-2xl shadow-2xl object-cover"
      />
      <p class="text-center text-gray-400 italic mt-6 text-lg">
        Here are some of the premium Notion templates, PDF companions, brand identities, thumbnails, cover art, and product visuals created for Osof Notion — clean, modern, and crafted to help creators scale their businesses with confidence and clarity.
      </p>
    </div>

    <h3 class="text-2xl font-semibold mt-16 mb-5">Opportunity</h3>
    <p class="mb-7 leading-relaxed">
      This was a chance to create a premium digital product ecosystem from scratch — combining beautiful Notion templates, downloadable PDF guides, a high-converting Gumroad store, and a custom-build service for clients who want done-for-you operations systems.
    </p>
    <p class="mb-7 leading-relaxed">
      I handled everything: ideation, template design, visual branding, product photography/mockups, copywriting, store setup, pricing strategy, checkout optimization, and client delivery workflow.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Impact</h3>
    <p class="mb-7 leading-relaxed">
      The store quickly gained traction with creators and small business owners looking for polished, ready-to-use Notion systems. Premium templates consistently receive high ratings and repeat purchases. The custom build service opened a high-ticket revenue stream, while the overall brand positioning helped establish trust and authority in the Notion + creator economy space.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Core Skills</h3>
    <div class="flex flex-wrap gap-3 mb-12">
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Notion Templates</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Gumroad Store Design</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">E-Commerce Setup</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Product Visuals</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">PDF Guide Design</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Custom Builds</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Branding</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Adobe Suites</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Canva</span>
    </div>
  `
}
else if (slug === 'maxx-improve-ecommerce') {
  projectContent.value = `
    <h2 class="text-3xl md:text-4xl font-bold mt-2 mb-10 text-orange-400">
      Power isn't just what you have — it's how you use it.
    </h2>

    <div class="grid md:grid-cols-2 gap-10 mb-14 text-gray-300">
      <div>
        <h3 class="text-xl font-semibold mb-4 text-white">Key Facts</h3>
        <ul class="space-y-2">
          <li><strong>Position:</strong> Creative Director</li>
          <li><strong>Period:</strong> 2023 – Present</li>
          <li><strong>Platform:</strong> Shopify solution with Custom CMS</li>
          <li><strong>Market:</strong> Successful launch across Europe and America</li>
          <li><strong>Integration:</strong> Custom CMS + Shopify</li>
        </ul>
      </div>
      <div>
        <p class="italic text-gray-400">
          A discreet, conversion-driven, user-friendly Shopify storefront built from scratch for a premium male wellness brand.
        </p>
      </div>
    </div>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Company</h3>
    <p class="mb-7 leading-relaxed">
      Maxx Improve is a Shopify-based eCommerce brand specializing in male enhancement products. The brand focuses on performance, overall wellbeing, and helping men improve confidence through science-backed, high-quality formulations. Maxx operates predominantly online and ships worldwide, prioritizing discretion, quality, and customer education to ensure safe, effective product use.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Challenge</h3>
    <p class="mb-7 leading-relaxed">
      When I joined the Maxx Improve project, the brand was facing several clear challenges:
    </p>
    <ul class="list-disc pl-6 space-y-3 mb-8 text-gray-300">
      <li><strong>No Existing Digital Presence:</strong> The brand was starting from scratch — no cohesive website that resonated with its target audience: men seeking discreet, reliable health solutions.</li>
      <li><strong>Sensitive Product Category:</strong> Selling male enhancement products online required careful, non-sensationalized messaging that was tasteful, discreet, and medically responsible.</li>
      <li><strong>Consistent Visual Identity:</strong> Maxx lacked a unified visual language — from hero images and product photos to icons, illustrations, banners, and overall site design.</li>
      <li><strong>Clear, Empathetic Copywriting:</strong> The brand needed website copy that would be reassuring, straightforward, and trustworthy — addressing potential concerns or doubts in a comforting way.</li>
    </ul>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Details</h3>
    <p class="mb-8 leading-relaxed">
      A clean, minimal, and conversion-driven Shopify storefront designed from scratch for Maxx Improve. The goal was to offer a discreet, user-friendly experience — intentionally structured for clarity, simplicity, and ease of navigation, while communicating the brand’s message of confidence and wellness without overwhelming the visitor.
    </p>

    <!-- First Hero Image + Caption -->
    <div class="mt-16 mb-20">
      <img 
        src="/images/projects/maxx-improve-ecommerce/hero-1.png"
        alt="Maxx Improve Shopify storefront"
        class="w-full rounded-2xl shadow-2xl object-cover"
      />
      <p class="text-center text-gray-400 italic mt-6 text-lg">
        A clean, minimal, and conversion-driven Shopify store for Maxx Improve — designed to offer a seamless, discreet, and user-friendly experience for customers. Every page is intentionally structured for clarity, simplicity, and ease of navigation, ensuring the brand’s message of confidence and wellness is communicated without overwhelming or intimidating the visitor.
      </p>
    </div>

    <!-- Second Hero Image + Caption -->
    <div class="mt-16 mb-20">
      <img 
        src="/images/projects/maxx-improve-ecommerce/hero-2.png"
        alt="Maxx Improve digital assets"
        class="w-full rounded-2xl shadow-2xl object-cover"
      />
      <p class="text-center text-gray-400 italic mt-6 text-lg">
        A cohesive collection of digital assets crafted for the Maxx Improve Shopify store — from intuitive iconography and product visuals to measurement diagrams and instructional graphics. Designed with purpose, each element reinforces the brand’s welcoming, professional feel while clearly passing across essential information in a discreet and visually appealing way.
      </p>
    </div>

    <h3 class="text-2xl font-semibold mt-16 mb-5">Opportunity</h3>
    <p class="mb-7 leading-relaxed">
      This project presented an opportunity to shape the entire digital experience for Maxx Improve’s customers:
    </p>
    <ul class="list-disc pl-6 space-y-2 mb-8 text-gray-300">
      <li>Build a discreet, conversion-driven Shopify storefront from scratch</li>
      <li>Design a layout that feels clear and trustworthy for both mobile and desktop users</li>
      <li>Create all digital assets — hero banners, product photos, icons, illustrations, banners</li>
      <li>Develop empathetic, professional copywriting that aligns with the brand voice</li>
    </ul>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Impact</h3>
    <p class="mb-7 leading-relaxed">
      The result is a cohesive, polished digital presence that elevated Maxx Improve’s position in the market:
    </p>
    <ul class="list-disc pl-6 space-y-2 mb-8 text-gray-300">
      <li>Successful Shopify launch with clean, trustworthy customer experience</li>
      <li>Digital assets contributed to brand consistency, professionalism, and trust</li>
      <li>Improved conversion rates through clear messaging and frictionless navigation</li>
      <li>Strong foundation for online growth, repeat purchases, and brand loyalty</li>
    </ul>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Core Skills</h3>
    <div class="flex flex-wrap gap-3 mb-12">
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Premium Design</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Minimal Design</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Innovation</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Premium Publishing</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">UX/UI</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">E-Commerce</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">User Testing</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Market Analysis</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Shopify</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">CMS Solution</span>
    </div>
  `
}
else if (slug === 'pumpfiat') {
  projectContent.value = `
    <h2 class="text-3xl md:text-4xl font-bold mt-2 mb-10 text-orange-400">
      From zero to launch — structured execution that made it happen.
    </h2>

    <div class="grid md:grid-cols-2 gap-10 mb-14 text-gray-300">
      <div>
        <h3 class="text-xl font-semibold mb-4 text-white">Key Facts</h3>
        <ul class="space-y-2">
          <li><strong>Role:</strong> Project Manager & Coordinator</li>
          <li><strong>Period:</strong> 2023 – 2024</li>
          <li><strong>Platform:</strong> Vue.js frontend + backend integration</li>
          <li><strong>Impact:</strong> Took the project from bootstrap to live launch</li>
          <li><strong>Website:</strong> <a href="https://pumpfiat.com" target="_blank" class="text-orange-400 hover:underline">pumpfiat.com</a></li>
          <li><strong>Revenue:</strong> Averages ~$30,000/month</li>
          <li><strong>Headquarters:</strong> Kansas City, MO</li>
        </ul>
      </div>
      <div>
        <p class="italic text-gray-400">
          Led cross-functional coordination, delivery, and launch of a permission-based outreach platform that provides verified prospect datasets and campaign tools for compliant, high-deliverability growth.
        </p>
      </div>
    </div>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Company</h3>
    <p class="mb-7 leading-relaxed">
      PumpFiat is a B2B SaaS company offering a permission-based outreach platform that helps businesses access verified prospect datasets and execute high-deliverability email campaigns. The product combines clean data sourcing, compliance-first tools, and campaign management features to enable scalable, ethical outbound growth. Headquartered in Kansas City, Missouri, PumpFiat serves clients across South Africa, Singapore, Germany, and beyond.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Challenge</h3>
    <p class="mb-7 leading-relaxed">
      The project started in bootstrap mode — early concept, scattered tasks, no clear delivery structure, and multiple moving parts across product, design, development, and operations. The biggest risk was losing momentum or shipping something that didn't meet the high standard required for a compliance-sensitive product in a competitive space.
    </p>
    <p class="mb-7 leading-relaxed">
      The goal was to bring structure, clarity, and speed — turning vision into a functional, live product without compromising quality, timelines, or team alignment.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Role & Contribution</h3>
    <p class="mb-7 leading-relaxed">
      I served as Project Manager and Coordinator, bringing my full experience in cross-functional delivery to the table. I owned the end-to-end process from bootstrap to launch:
    </p>
    <ul class="list-disc pl-6 space-y-3 mb-8 text-gray-300">
      <li>Created the project structure, timelines, milestones, and tracking system</li>
      <li>Coordinated between product, design, development, and stakeholders</li>
      <li>Ensured alignment on priorities, scope, and deliverables</li>
      <li>Managed risks, blockers, and dependencies in real time</li>
      <li>Led sprint planning, daily standups, and progress reviews</li>
      <li>Played a critical role in decision-making and keeping momentum high</li>
      <li>Delivered the platform live — on time and to quality standard</li>
    </ul>
    <p class="mb-7 leading-relaxed">
      The experience working with experts from South Africa, Singapore, Germany, and the US was incredibly rewarding — it reinforced how structured execution and global collaboration can turn a strong idea into a high-performing B2B SaaS product averaging ~$30,000/month.
    </p>

    <!-- Hero image + caption -->
    <div class="mt-16 mb-20">
      <img 
        src="/images/projects/pumpfiat/hero-main.png"
        alt="PumpFiat platform overview"
        class="w-full rounded-2xl shadow-2xl object-cover"
      />
      <p class="text-center text-gray-400 italic mt-6 text-lg">
        From early bootstrap to a live B2B SaaS platform averaging $30,000/month — a permission-based outreach tool serving clients across South Africa, Singapore, Germany, and beyond. Built with Vue.js, delivered through structured coordination, and scaled with global expertise from Kansas City HQ.
      </p>
    </div>

    <h3 class="text-2xl font-semibold mt-16 mb-5">Impact</h3>
    <p class="mb-7 leading-relaxed">
      The project launched successfully and is now live at <a href="https://pumpfiat.com" target="_blank" class="text-orange-400 hover:underline">pumpfiat.com</a>. My structured approach and coordination were critical in turning an early-stage idea into a functional, user-facing product — delivered on time, within scope, and with high quality.
    </p>
    <p class="mb-7 leading-relaxed">
      The platform now provides real value to users, averaging ~$30,000/month in revenue, and the experience reinforced my belief in the power of clear execution when building in bootstrap mode with international teams.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Core Skills</h3>
    <div class="flex flex-wrap gap-3 mb-12">
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Project Management</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Cross-Functional Coordination</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Bootstrap Delivery</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Stakeholder Alignment</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Risk & Dependency Management</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Launch Execution</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Vue.js Ecosystem</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Global Team Collaboration</span>
    </div>
  `
}
else if (slug === 'compasspdf') {
  projectContent.value = `
    <h2 class="text-3xl md:text-4xl font-bold mt-2 mb-10 text-orange-400">
      Your world — unlocked, one country at a time.
    </h2>

    <div class="grid md:grid-cols-2 gap-10 mb-14 text-gray-300">
      <div>
        <h3 class="text-xl font-semibold mb-4 text-white">Key Facts</h3>
        <ul class="space-y-2">
          <li><strong>Role:</strong> Creative Director, Designer & Full Product Creator</li>
          <li><strong>Platform:</strong> Gumroad</li>
          <li><strong>Period:</strong> 2024 – Present</li>
          <li><strong>Impact:</strong> Premium country-specific travel PDFs sold globally</li>
          <li><strong>Products:</strong> Detailed guides for visas, culture, costs, safety & more</li>
        </ul>
      </div>
      <div>
        <p class="italic text-gray-400">
          A collection of beautifully designed, comprehensive country travel PDFs that help people plan confident, informed, and unforgettable trips — from visa rules to wild experiences.
        </p>
      </div>
    </div>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Company</h3>
    <p class="mb-7 leading-relaxed">
      Compass PDF is a Gumroad-powered digital product line offering premium, country-specific travel guides. Each PDF is a complete planning companion — covering visa requirements, entry rules, costs, best seasons, festivals, safety tips, local customs, accommodation hacks, currency exchange, digital nomad/student visa info, and unforgettable experiences. Designed for travelers who want clarity, confidence, and inspiration before they book a single flight.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Challenge</h3>
    <p class="mb-7 leading-relaxed">
      Travelers often face scattered, outdated, or overwhelming information when planning trips — especially to countries with complex visa rules, cultural nuances, or hidden costs. Free online sources are fragmented, while generic guidebooks feel impersonal and outdated quickly.
    </p>
    <p class="mb-7 leading-relaxed">
      The opportunity was to create a premium, beautifully designed, always-up-to-date digital product that feels like having a personal travel expert: clear, visual, actionable, and emotionally inspiring — sold directly on Gumroad for instant access.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Details</h3>
    <p class="mb-8 leading-relaxed">
      I built the entire Compass PDF experience from scratch: designed every country guide (layout, visuals, tables, maps, icons), wrote empathetic and practical copy, created consistent branding across PDFs, thumbnails, covers, and Gumroad product pages, and structured each guide to answer every major planning question in one beautiful download.
    </p>

    <!-- Hero image + caption -->
    <div class="mt-16 mb-20">
      <img 
        src="/images/projects/compasspdf/hero-main.png"
        alt="Compass PDF country travel guides"
        class="w-full rounded-2xl shadow-2xl object-cover"
      />
      <p class="text-center text-gray-400 italic mt-6 text-lg">
        A premium collection of country-specific travel PDFs — each one thoughtfully designed with clear layouts, vibrant visuals, practical tables, cultural insights, and inspiring highlights. From visa rules and costs to festivals, safety, and wild experiences — everything travelers need in one elegant, downloadable guide.
      </p>
    </div>

    <h3 class="text-2xl font-semibold mt-16 mb-5">Opportunity</h3>
    <p class="mb-7 leading-relaxed">
      This project allowed me to create a scalable digital product ecosystem: high-value PDFs that solve real pain points for travelers while building a premium brand on Gumroad. I handled full-cycle creation — research, copywriting, design, visual identity, product mockups, Gumroad storefront setup, pricing strategy, and launch assets.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-5">Impact</h3>
    <p class="mb-7 leading-relaxed">
      The Compass PDF series quickly became a go-to resource for travelers planning trips to complex or culturally rich destinations. Each guide delivers instant value, builds trust through clarity and beauty, and drives repeat purchases as people return for new countries. The brand positioning as "your personal travel expert in one download" has helped establish authority and loyalty in the digital travel product space.
    </p>

    <h3 class="text-2xl font-semibold mt-14 mb-6">Core Skills</h3>
    <div class="flex flex-wrap gap-3 mb-12">
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Product Design</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Gumroad Store</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">PDF Layout</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Travel Content</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Branding</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Visual Storytelling</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">E-Commerce</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Adobe Suites</span>
      <span class="px-4 py-2 bg-[#0D1B2A] border border-[#1E2D3D] rounded-lg text-sm">Canva</span>
    </div>
  `
}
})
const currentSlide = ref(0)
const pauseAuto = ref(false)

// Auto-play (every 5 seconds)
let interval = null
onMounted(() => {
  interval = setInterval(() => {
    if (!pauseAuto.value) {
      currentSlide.value = (currentSlide.value + 1) % 10
    }
  }, 5000)
})

onUnmounted(() => {
  clearInterval(interval)
})

// Manual navigation
const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % 10
}
const prevSlide = () => {
  currentSlide.value = (currentSlide.value - 1 + 10) % 10
}

</script>

<style scoped>
.prose h2 {
  @apply text-3xl md:text-4xl font-bold mt-16 mb-8 text-orange-400;
}
.prose h3 {
  @apply text-2xl font-semibold mt-14 mb-6 text-white;
}
.prose p {
  @apply text-gray-300 leading-relaxed mb-7 text-[1.05rem];
}
.prose blockquote {
  @apply text-lg italic border-l-4 border-orange-500 pl-6 my-12 py-1;
}
</style>
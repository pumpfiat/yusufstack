<template>
  <div class="gists-content">
    <div
      v-for="(item, index) in testimonials"
      :key="index"
      class="gist-wrapper"
    >
      <!-- Header (like your snippet header) -->
      <div class="gist-header">
        <div class="user">
          <img :src="item.avatar" class="avatar" />
          <div>
            <div class="username">@{{ item.username }}</div>
            <div class="meta">
              {{ item.name }} • {{ item.company }}
            </div>
          </div>
        </div>
      </div>

      <!-- Code Box -->
      <div class="gist-box">
<pre><code>// testimonial
/*
{{ item.text }}
*/
</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
const testimonials = [
  {
    username: "snehauncover",
    name: "Sneha Mehta",
    company: "Founder • Uncover Skincare",
    avatar: "/images/testimonials/sneha.png",
    text: "Yusuf came into our brand at a pivotal time — right as we were expanding from Kenya into West Africa. His design work for our product materials helped us communicate skincare across cultural lines, helping us create tools that connected with new customers while staying true to our values. Beyond the visuals, Yusuf provided crucial strategic advice that made our entry into new markets feel less overwhelming. We couldn’t have asked for better support."
  },
  {
    username: "sofitngr",
    name: "Sandra Okeke",
    company: "Founder • Sofit NGR",
    avatar: "/images/testimonials/sandra.png",
    text: "Running a brand while creating content full-time can be overwhelming, but Yusuf made everything easier. He captured my brand perfectly — clean, motivating, and accessible."
  },
  {
    username: "maxximprove",
    name: "Robin Oosterbosch",
    company: "Founder • Maxx Improve",
    avatar: "/images/testimonials/robin.png",
    text: "I've worked with creatives across Europe, but Yusuf stood out. His detail matched agencies in the €50,000 range. Smooth process. Exceptional results."
  },
  {
    username: "kaijego",
    name: "Alma Asinobi",
    company: "Founder • Kaijego",
    avatar: "/images/testimonials/alma.png",
    text: "Working with Yusuf on 'Around the World with Alma Asinobi' was intuitive and seamless. The final design captured Kaijego beautifully."
  },
  {
    username: "CTG-Method",
    name: "Dr. Esther Makaripe",
    company: "Founder • Certified Traders Group (CTG)",
    avatar: "/images/testimonials/Esther.png",
    text: "Working with Yusuf has been an incredible experience. He reached out to us out of the blue and, before ever joining the project, had already identified opportunities within our platform and presented thoughtful solutions that aligned with our vision.\n\nWhat impressed me most was how quickly he integrated with our team. Without a lengthy onboarding process, he was able to collaborate effectively with our developers, understand the product, and deliver meaningful work for our audience in just four weeks."
  },
  {
    username: "rroomfies",
    name: "Jane Tsang",
    company: "Finance Influencer • rroomfies",
    avatar: "/images/testimonials/Jane.png",
    text: "I first discovered Yusuf through one of his Notion products, and I was genuinely blown away by the level of thought, detail, and usability behind it. It immediately stood out from anything else I had used, so when I needed a custom system tailored to my own brand and audience, he was the first person I reached out to.\n\nYusuf didn't just deliver what I asked for—he built something that became incredibly valuable to my community. So many people reached out asking where they could get it or how they could work with him because of how useful and well-designed it was."
  }
]
</script>

<style scoped>
.gists-content {
  padding: 2rem;
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
}

/* Wrapper */
.gist-wrapper {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

/* Header */
.gist-header {
  display: flex;
  align-items: center;
}

.user {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

/* Avatar */
.avatar {
  width: 38px;
  height: 38px;
  border-radius: 50%;
  object-fit: cover;
}

/* Username */
.username {
  color: #60A5FA;
  font-size: 0.9rem;
  font-weight: 500;
}

/* Meta */
.meta {
  font-size: 0.8rem;
  color: #607B96;
}

/* Code Box */
.gist-box {
  background: #011627;
  border: 1px solid #1E2D3D;
  border-radius: 12px;
  padding: 1.25rem;
  transition: border 0.3s ease;
}

.gist-box:hover {
  border-color: #FEA55F;
}

pre {
  margin: 0;
  white-space: pre-wrap;
  word-break: break-word;
  overflow-wrap: anywhere;
  font-family: 'Fira Code Retina', 'Fira Code', monospace;
  font-size: 0.85rem;
  line-height: 1.6;
  color: #C9D1D9;
  -webkit-font-smoothing: antialiased;
}

code {
  color: #C9D1D9;
  font-family: inherit;
}
</style>

<template>
  <main id="contact-me" class="page flex h-screen overflow-hidden">

    <!-- LEFT SIDEBAR -->
    <div id="page-menu"
         class="w-80 flex flex-col border-right overflow-y-auto">

      <!-- Mobile Title -->
      <div id="mobile-page-title" class="lg:hidden p-4">
        <h2>_contact-me</h2>
      </div>

      <!-- Contacts -->
      <div id="contacts" class="submenu">
        <div class="title" @click="open('contacts')">
          <img class="arrow" src="/icons/arrow.svg" />
          <h3>contacts</h3>
        </div>

        <div class="links">
          <div class="link">
            <img src="/icons/email.svg" />
            <a href="mailto:yt@yusufstack.com"
               class="font-fira_retina text-menu-text hover:text-white">
              yt@yusufstack.com
            </a>
          </div>

          <div class="link">
            <img src="/icons/phone.svg" />
            <a href="tel:+2348088374961"
               class="font-fira_retina text-menu-text hover:text-white">
              +234 808 837 4961
            </a>
          </div>
        </div>
      </div>

      <!-- Passport Photo -->
      <div id="find-me-in" class="submenu border-top">
        <div class="title" @click="open('find-me-in')">
          <img class="arrow" src="/icons/arrow.svg" />
          <h3>passport photo</h3>
        </div>

        <div class="links p-6 flex justify-center">
          <img src="/images/passport/yusuf.jpg"
               alt="Yusuf Taiwo"
               class="w-64 md:w-72 object-cover rounded-2xl border-4 border-[#1E2D3D] shadow-2xl transition-all duration-300 hover:border-orange-500" />
        </div>
      </div>

    </div>

    <!-- RIGHT MAIN CONTENT -->
    <div class="flex-1 flex flex-col overflow-hidden">

      <!-- Desktop Tab -->
      <div class="tab-height hidden lg:flex border-bot items-center px-4">
        <p class="font-fira_regular text-menu-text text-sm">
          contacts
        </p>
      </div>

      <!-- CONTENT GRID -->
      <div class="flex-1 lg:grid lg:grid-cols-2 min-h-0">

        <!-- LEFT FORM -->
        <div class="border-right overflow-y-auto p-6">
            <ContactForm
  v-model:name="name"
  v-model:email="email"
  v-model:message="message" />


        </div>

        <!-- RIGHT CODE PREVIEW -->
        <div class="hidden lg:flex flex-col overflow-hidden">

          <div class="flex-1 overflow-y-auto p-10">
            <FormContentCode
              :name="name"
              :email="email"
              :message="message" />
          </div>

        </div>

      </div>

    </div>

  </main>
</template>


<script>
import DevConfig from '~/developer.json';
export default {
    data() {
        return {
            name: '',
            email: '',
            message: '',
        }
    },
    setup() {
        return {
            contact: DevConfig.contacts,
        }
    },
    methods: {
        open(elementId) {
            const element = document.getElementById(elementId);
            const arrow = element.querySelector('.arrow');
            const links = element.querySelector('.links');

            if (links.style.display === 'block') {
                links.style.display = 'none';
                arrow.style.transform = 'rotate(0deg)';
            } else {
                links.style.display = 'block';
                arrow.style.transform = 'rotate(90deg)';
            }
        }
    },
    mounted() {
  // Wait for DOM to be fully updated
  this.$nextTick(() => {
    const submenus = document.querySelectorAll('.submenu');

    submenus.forEach(submenu => {
      const linksEl = submenu.querySelector('.links') || submenu.querySelector('#links');
      const arrowEl = submenu.querySelector('.arrow');

      if (!linksEl || !arrowEl) return; // skip if missing

      if (window.innerWidth > 1024) {
        linksEl.style.display = 'block';
        arrowEl.style.transform = 'rotate(90deg)';
      } else {
        linksEl.style.display = 'none';
        arrowEl.style.transform = 'rotate(0deg)';
      }
    });
  });

  // Your existing input listeners...
  const nameInput = document.getElementById('name-input');
  // ... rest of your code ...
},

}
</script>

<style>

.arrow {
    transition: 0.1s;
    margin-right: 10px;
    width: 9px;
    height: 9px;
}

.submenu {
    display: flex;
    flex-direction: column;
}

.submenu .title h3 {
    @apply font-fira_regular;
    color: white;
    font-size: 16px;
}

.link {
    display: flex;
    align-items: center;
    padding: 4px 25px;
}

.link img {
    width: 16px;
    height: 16px;
    margin-right: 10px;
}

#links {
    padding: 10px 0px;
}

.form-content {
    padding: 75px 50px 0px 75px;
    width: 100%;
    height: 100%;
    overflow-y: auto;
    font-size: 15px;
}
@media (min-width: 1024px) {
    
    .submenu .title {
        display: flex;
        align-items: center;
        border-bottom: 1px solid #1E2D3D;
        padding: 0px 25px;
        height: 35px;
        padding: 0px 25px;
    }
    .submenu .title:hover {
        cursor: pointer;
    }
    .submenu .title h3 {
        font-size: 14px;
    }
}

</style>
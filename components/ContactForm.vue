<template>
  <form id="contact-form" class="text-sm" @submit.prevent="handleSubmit">

    <div class="flex flex-col">
      <label for="name-input" class="mb-3">_name:</label>
      <input
        id="name-input"
        type="text"
        :value="name"
        @input="$emit('update:name', $event.target.value)"
        class="p-2 mb-5 placeholder-slate-600"
        placeholder="Your name"
        required
      />
    </div>

    <div class="flex flex-col">
      <label for="email-input" class="mb-3">_email:</label>
      <input
        id="email-input"
        type="email"
        :value="email"
        @input="$emit('update:email', $event.target.value)"
        class="p-2 mb-5 placeholder-slate-600"
        placeholder="your@email.com"
        required
      />
    </div>

    <div class="flex flex-col">
      <label for="message-input" class="mb-3">_message:</label>
      <textarea
        id="message-input"
        :value="message"
        @input="$emit('update:message', $event.target.value)"
        class="placeholder-slate-600"
        placeholder="Write your message..."
        required
      ></textarea>
    </div>

    <button
      id="submit-button"
      type="submit"
      class="py-2 px-4"
    >
      submit-message
    </button>

  </form>
</template>

<script>
import emailjs from "@emailjs/browser";
export default {
  name: "ContactForm",

  props: {
    name: {
      type: String,
      required: true,
    },
    email: {
      type: String,
      required: true,
    },
    message: {
      type: String,
      required: true,
    },
  },

  emits: ["update:name", "update:email", "update:message"],

  methods: {
   handleSubmit() {
  emailjs.send(
    "service_1h7nygd",
    "template_x7r6rub",
    {
      from_name: this.name,
      from_email: this.email,
      message: this.message,
    },
    "Iu07qXdbpq1Mocost"
  )
  .then(() => {
    alert("Message sent successfully 🚀");

    // 🔥 Reset fields by emitting empty values
    this.$emit("update:name", "");
    this.$emit("update:email", "");
    this.$emit("update:message", "");
  })
  .catch((error) => {
    console.error("FAILED...", error);
    alert("Something went wrong ❌");
  });
}
,
  },
};
</script>

<style>

form {
  @apply font-fira_retina text-menu-text;
}

input {
  background-color: #011221;
  border: 2px solid #1E2D3D;
  border-radius: 7px;
}

#message-input {
  background-color: #011221;
  border: 2px solid #1E2D3D;
  border-radius: 7px;
  resize: none;
  height: 150px;
  padding: 10px;
}

#submit-button {
  @apply font-fira_retina text-white text-sm;
  background-color: #1E2D3D;
  border-radius: 7px;
  margin-top: 20px;
  cursor: pointer;
}

#submit-button:hover {
  background-color: #263B50;
}

input:focus,
#message-input:focus {
  outline: none;
  border: 2px solid #607b96;
  box-shadow: #607b9669 0px 0px 0px 2px;
}

#contact-form {
  max-width: 370px;
  width: 100%;
}

@media (max-width: 1920px) {
  #contact-form {
    max-width: 320px;
  }

  #submit-button {
    font-size: 12px;
  }

  textarea {
    font-size: 13px;
    max-height: 130px !important;
  }

  input {
    font-size: 13px;
  }
}

</style>

<template>
  <div class="contact-container py-8 sm:py-12 lg:py-16">
    <div class="container mx-auto px-4 sm:px-6 lg:px-8">
      <div class="section-header mb-8 sm:mb-10 lg:mb-12">
        <h1 class="text-center font-bold text-3xl sm:text-4xl lg:text-5xl mb-3 text-white">
          Contact Me
        </h1>
        <div class="w-20 sm:w-24 h-1 bg-blue-500 mx-auto mb-4 sm:mb-6"></div>
        <p class="text-center text-gray-300 max-w-xl sm:max-w-2xl mx-auto text-sm sm:text-base px-4">
          Feel free to reach out! I'm always open to discussing new projects,
          creative ideas or opportunities to be part of your vision.
        </p>
      </div>

      <div class="contact-content">
        <div class="contact-info">
          <div class="contact-card">
            <div class="contact-card-header">
              <h2 class="text-xl sm:text-2xl font-bold mb-3 sm:mb-4">Let's Connect</h2>
              <p class="text-gray-300 mb-4 sm:mb-6 text-sm sm:text-base">
                I'm currently available for freelance work or full-time
                positions. If you have a project that needs some creative work,
                don't hesitate to contact me.
              </p>
            </div>

            <div class="contact-methods">
              <div
                class="contact-method"
                @mouseenter="activeMethod = 'email'"
                @mouseleave="activeMethod = null"
              >
                <div
                  class="contact-icon"
                  :class="{ active: activeMethod === 'email' }"
                >
                  <Icon name="ic:sharp-mail" />
                </div>

                <div class="contact-details">
                  <h3>Email</h3>
                  <p class="break-all">cheng.menglay79@gmail.com</p>
                </div>
              </div>

              <div
                class="contact-method"
                @mouseenter="activeMethod = 'linkedin'"
                @mouseleave="activeMethod = null"
              >
                <div
                  class="contact-icon"
                  :class="{ active: activeMethod === 'linkedin' }"
                >
                  <Icon name="devicon:linkedin" />
                </div>
                <div class="contact-details">
                  <h3>LinkedIn</h3>
                  <NuxtLink
                    to="https://bit.ly/chengmenglay"
                    target="_blank"
                    class="contact-link break-all"
                  >
                    bit.ly/chengmenglay
                  </NuxtLink>
                </div>
              </div>

              <div
                class="contact-method"
                @mouseenter="activeMethod = 'github'"
                @mouseleave="activeMethod = null"
              >
                <div
                  class="contact-icon"
                  :class="{ active: activeMethod === 'github' }"
                >
                  <Icon name="uiw:github" />
                </div>
                <div class="contact-details">
                  <h3>GitHub</h3>
                  <NuxtLink
                    to="https://github.com/ChengMenglay"
                    target="_blank"
                    class="contact-link break-all"
                  >
                    github.com/ChengMenglay
                  </NuxtLink>
                </div>
              </div>
              
              <div
                class="contact-method"
                @mouseenter="activeMethod = 'telegram'"
                @mouseleave="activeMethod = null"
              >
                <div
                  class="contact-icon"
                  :class="{ active: activeMethod === 'telegram' }"
                >
                  <Icon name="mdi:telegram" />
                </div>
                <div class="contact-details">
                  <h3>Telegram</h3>
                  <NuxtLink
                    to="https://t.me/Cheng_Meglay"
                    target="_blank"
                    class="contact-link break-all"
                  >
                    t.me/Cheng_Meglay
                  </NuxtLink>
                </div>
              </div>
              
              <div
                class="contact-method"
                @mouseenter="activeMethod = 'facebook'"
                @mouseleave="activeMethod = null"
              >
                <div
                  class="contact-icon"
                  :class="{ active: activeMethod === 'facebook' }"
                >
                  <Icon name="devicon:facebook" />
                </div>
                <div class="contact-details">
                  <h3>Facebook</h3>
                  <NuxtLink
                    to="https://www.facebook.com/cheng.menglay"
                    target="_blank"
                    class="contact-link break-all"
                  >
                    facebook.com/cheng.menglay
                  </NuxtLink>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <div class="contact-form">
          <div class="form-card">
            <h2 class="text-xl sm:text-2xl font-bold mb-3 sm:mb-4">Send Me a Message</h2>

            <div v-if="emailStatus.success" class="success-message">
              <p>Thank you! Your message has been sent successfully.</p>
            </div>

            <div v-if="emailStatus.error" class="error-message text-red-400">
              <p>{{ emailStatus.errorMsg }}</p>
            </div>

            <form @submit.prevent="sendEmail" v-if="!emailStatus.success">
              <div class="form-group">
                <label for="name">Your Name</label>
                <div class="input-container">
                  <Icon name="mdi:account" class="input-icon" />
                  <input
                    type="text"
                    id="name"
                    v-model="formData.name"
                    placeholder="John Doe"
                    required
                  />
                </div>
              </div>

              <div class="form-group">
                <label for="email">Your Email</label>
                <div class="input-container">
                  <Icon name="mdi:email" class="input-icon" />
                  <input
                    type="email"
                    id="email"
                    v-model="formData.email"
                    placeholder="john@example.com"
                    required
                  />
                </div>
              </div>

              <div class="form-group">
                <label for="subject">Subject</label>
                <div class="input-container">
                  <Icon name="mdi:text-subject" class="input-icon" />
                  <input
                    type="text"
                    id="subject"
                    v-model="formData.subject"
                    placeholder="Project Inquiry"
                    required
                  />
                </div>
              </div>

              <div class="form-group">
                <label for="message">Message</label>
                <div class="input-container textarea">
                  <Icon name="mdi:message-text" class="input-icon" />
                  <textarea
                    id="message"
                    rows="5"
                    v-model="formData.message"
                    placeholder="Your message here..."
                    required
                  ></textarea>
                </div>
              </div>

              <button type="submit" class="submit-button" :disabled="sending">
                <span>{{ sending ? "Sending..." : "Send Message" }}</span>
                <Icon name="mdi:send" />
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import emailjs from "@emailjs/browser";
const config = useRuntimeConfig();

const activeMethod = ref(null);

// Form data
const formData = ref({
  name: "",
  email: "",
  subject: "",
  message: "",
});

// Email status
const sending = ref(false);
const emailStatus = ref({
  success: false,
  error: false,
  errorMsg: "",
});

// Send email function
const sendEmail = async () => {
  sending.value = true;
  emailStatus.value = {
    success: false,
    error: false,
    errorMsg: "",
  };

  try {
    const result = await emailjs.send(
      config.public.SERVICE_ID,
      config.public.TEMPLATE_ID,
      {
        from_name: formData.value.name,
        from_email: formData.value.email,
        subject: formData.value.subject,
        message: formData.value.message,
      },
      config.public.PUBLIC_KEY
    );

    if (result.status === 200) {
      emailStatus.value.success = true;
      // Reset form
      formData.value = {
        name: "",
        email: "",
        subject: "",
        message: "",
      };
    }
  } catch (error) {
    emailStatus.value.error = true;
    emailStatus.value.errorMsg =
      "Sorry, there was an error sending your message. Please try again later.";
    console.error("Email error:", error);
  } finally {
    sending.value = false;
  }
};
</script>

<style scoped>
.contact-container {
  background: linear-gradient(135deg, #0f172a 0%, #1e3a8a 100%);
  position: relative;
  overflow: hidden;
  min-height: 100vh;
}

.contact-container::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(
    circle at 80% 50%,
    rgba(59, 130, 246, 0.1) 0%,
    transparent 50%
  );
}

.contact-content {
  display: grid;
  grid-template-columns: 1fr;
  gap: 20px;
  max-width: 1200px;
  margin: 0 auto;
  position: relative;
  z-index: 1;
}

/* Desktop and larger tablets */
@media (min-width: 1024px) {
  .contact-content {
    grid-template-columns: 1fr 1fr;
    gap: 30px;
  }
}

/* Medium tablets */
@media (min-width: 768px) and (max-width: 1023px) {
  .contact-content {
    grid-template-columns: 1fr;
    gap: 25px;
    max-width: 600px;
  }
}

.contact-card,
.form-card {
  background: rgba(15, 23, 42, 0.9);
  border-radius: 12px;
  border: 1px solid rgba(59, 130, 246, 0.3);
  padding: 20px;
  height: 100%;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
  backdrop-filter: blur(10px);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

@media (min-width: 640px) {
  .contact-card,
  .form-card {
    padding: 25px;
  }
}

@media (min-width: 1024px) {
  .contact-card,
  .form-card {
    padding: 30px;
  }
}

.contact-card:hover,
.form-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.3);
  border-color: rgba(59, 130, 246, 0.5);
}

.contact-methods {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

@media (min-width: 640px) {
  .contact-methods {
    gap: 20px;
  }
}

.contact-method {
  display: flex;
  align-items: center;
  padding: 12px;
  border-radius: 8px;
  background: rgba(30, 41, 59, 0.5);
  transition: all 0.3s ease;
}

@media (min-width: 640px) {
  .contact-method {
    padding: 15px;
  }
}

.contact-method:hover {
  background: rgba(30, 41, 59, 0.8);
}

@media (min-width: 768px) {
  .contact-method:hover {
    transform: translateX(10px);
  }
}

.contact-icon {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: rgba(59, 130, 246, 0.2);
  margin-right: 12px;
  font-size: 20px;
  color: #60a5fa;
  transition: all 0.3s ease;
  flex-shrink: 0;
}

@media (min-width: 640px) {
  .contact-icon {
    width: 50px;
    height: 50px;
    margin-right: 15px;
    font-size: 24px;
  }
}

.contact-icon.active {
  background: #3b82f6;
  color: white;
  transform: scale(1.1);
}

.contact-details {
  flex: 1;
  min-width: 0;
}

.contact-details h3 {
  font-weight: 600;
  margin-bottom: 4px;
  color: white;
  font-size: 14px;
}

@media (min-width: 640px) {
  .contact-details h3 {
    margin-bottom: 5px;
    font-size: 16px;
  }
}

.contact-details p {
  color: #cbd5e1;
  font-size: 13px;
  word-wrap: break-word;
}

@media (min-width: 640px) {
  .contact-details p {
    font-size: 14px;
  }
}

.contact-link {
  color: #60a5fa;
  text-decoration: none;
  transition: color 0.3s ease;
  font-size: 13px;
  word-wrap: break-word;
}

@media (min-width: 640px) {
  .contact-link {
    font-size: 14px;
  }
}

.contact-link:hover {
  color: #93c5fd;
  text-decoration: underline;
}

.form-group {
  margin-bottom: 16px;
}

@media (min-width: 640px) {
  .form-group {
    margin-bottom: 20px;
  }
}

label {
  display: block;
  margin-bottom: 6px;
  font-weight: 500;
  color: #e2e8f0;
  font-size: 14px;
}

@media (min-width: 640px) {
  label {
    margin-bottom: 8px;
    font-size: 16px;
  }
}

.input-container {
  position: relative;
  display: flex;
  align-items: center;
}

.input-icon {
  position: absolute;
  left: 12px;
  color: #64748b;
  font-size: 18px;
  z-index: 2;
}

@media (min-width: 640px) {
  .input-icon {
    left: 15px;
    font-size: 20px;
  }
}

input,
textarea {
  width: 100%;
  padding: 10px 12px 10px 40px;
  border-radius: 8px;
  background: rgba(30, 41, 59, 0.5);
  border: 1px solid rgba(59, 130, 246, 0.3);
  color: white;
  font-size: 14px;
  transition: all 0.3s ease;
}

@media (min-width: 640px) {
  input,
  textarea {
    padding: 12px 15px 12px 45px;
    font-size: 16px;
  }
}

textarea {
  resize: none;
  min-height: 100px;
}

@media (min-width: 640px) {
  textarea {
    min-height: 120px;
  }
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3b82f6;
  background: rgba(30, 41, 59, 0.8);
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.2);
}

.input-container.textarea .input-icon {
  top: 10px;
}

@media (min-width: 640px) {
  .input-container.textarea .input-icon {
    top: 12px;
  }
}

.submit-button {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  width: 100%;
  padding: 12px 20px;
  background: #3b82f6;
  color: white;
  border: none;
  border-radius: 8px;
  font-weight: 600;
  font-size: 14px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

@media (min-width: 640px) {
  .submit-button {
    gap: 10px;
    font-size: 16px;
  }
}

.submit-button:hover:not(:disabled) {
  background: #2563eb;
  transform: translateY(-2px);
  box-shadow: 0 6px 10px rgba(0, 0, 0, 0.2);
}

.submit-button:active {
  transform: translateY(0);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.submit-button:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.success-message,
.error-message {
  padding: 12px;
  border-radius: 8px;
  margin-bottom: 16px;
  text-align: center;
  font-size: 14px;
}

@media (min-width: 640px) {
  .success-message,
  .error-message {
    margin-bottom: 20px;
    font-size: 16px;
  }
}

.success-message {
  background: rgba(34, 197, 94, 0.2);
  border: 1px solid rgba(34, 197, 94, 0.3);
  color: #86efac;
}

.error-message {
  background: rgba(239, 68, 68, 0.2);
  border: 1px solid rgba(239, 68, 68, 0.3);
}

/* Mobile-specific improvements */
@media (max-width: 639px) {
  .contact-form {
    order: 1;
  }

  .contact-info {
    order: 2;
  }

  .contact-method {
    flex-wrap: wrap;
  }

  .contact-details {
    overflow-wrap: break-word;
  }
}

/* Ensure proper spacing on very small screens */
@media (max-width: 360px) {
  .container {
    padding-left: 16px;
    padding-right: 16px;
  }

  .contact-card,
  .form-card {
    padding: 16px;
  }

  .contact-icon {
    width: 36px;
    height: 36px;
    font-size: 18px;
    margin-right: 10px;
  }
}
</style>
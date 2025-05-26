<template>
  <div>
    <header
      class="w-screen bg-blue-950 opacity-90 shadow-md shadow-blue-900 fixed top-0 z-10"
    >
      <nav
        class="container px-5 py-3 md:flex justify-between mx-auto items-center relative"
      >
        <NuxtLink to="/" class="text-bold text-3xl font-bold"
          >Portfolio</NuxtLink
        >
        <ul
          class="md:flex md:text-center md:gap-4 font-bold md:static absolute bg-blue-950 md:w-auto w-full top-16 duration-500 ease-in md:px-0 px-10"
          :class="[nav ? 'left-0' : 'left-[-130%]']"
        >
          <li
            v-for="(link, i) in links"
            class="md:my-0 my-6 hover:text-blue-500 duration-300"
            :key="i"
          >
            <NuxtLink :to="link.link">{{ link.name }}</NuxtLink>
          </li>
        </ul>
        <span
          class="text-3xl absolute md:hidden flex top-5 right-5"
          @click="nav = !nav"
        >
          <Icon name="fluent:navigation-24-filled"></Icon>
        </span>
      </nav>
      <div></div>
    </header>

    <!-- Display Page -->
    <div class="max-w-[1240px] mx-auto my-5">
      <slot />
    </div>

    <!-- Footer -->
    <footer
      class="bg-[#14213d] py-14 mt-40 flex flex-col items-center mx-3 relative"
    >
      <h1 class="text-center text-xl font-bold text-blue-600">Cheng Menglay</h1>
      <ul class="flex justify-center gap-4 font-bold mt-5">
        <li v-for="(link, i) in links" :key="i">
          <NuxtLink :to="link.link">{{ link.name }}</NuxtLink>
        </li>
      </ul>
      <ul class="flex justify-center gap-4 font-bold mt-5">
        <li>
          <NuxtLink to="https://www.facebook.com/cheng.menglay" target="_blank">
            <Icon name="logos:facebook" class="text-2xl"
          /></NuxtLink>
        </li>
        <li>
          <NuxtLink to="https://www.instagram.com/chengmenglay/" target="_blank"
            ><Icon name="skill-icons:instagram" class="text-2xl"
          /></NuxtLink>
        </li>
        <li>
          <NuxtLink to="https://bit.ly/chengmenglay" target="_blank">
            <Icon name="devicon:linkedin" class="text-2xl" />
          </NuxtLink>
        </li>
        <li>
          <NuxtLink to="https://t.me/Cheng_Meglay" target="_blank"
            ><Icon name="logos:telegram" class="text-2xl"
          /></NuxtLink>
        </li>
      </ul>
      <p class="text-center mt-5 text-gray-500">
        &copy; {{ new Date().getFullYear() }} Menglay Portfolio. All rights
        reserved.
      </p>
    </footer>

    <!-- Modern Scroll to Top Button -->
    <Transition name="scroll-btn">
      <button
        v-if="showScrollButton"
        @click="scrollToTop"
        class="scroll-to-top-btn"
        aria-label="Scroll to top"
        :class="{ 'scroll-btn-visible': showScrollButton }"
      >
        <div class="scroll-btn-icon">
          <Icon name="mdi:chevron-up" class="text-xl" />
        </div>
        <div class="scroll-btn-bg"></div>
        <div class="scroll-btn-progress">
          <svg class="progress-ring" width="56" height="56">
            <circle
              class="progress-ring-circle"
              cx="28"
              cy="28"
              r="24"
              :stroke-dasharray="circumference"
              :stroke-dashoffset="progressOffset"
            />
          </svg>
        </div>
      </button>
    </Transition>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed } from "vue";

const nav = ref(false);
const showScrollButton = ref(false);
const scrollProgress = ref(0);

const links = [
  { name: "Home", link: "#home" },
  { name: "Skill", link: "#skill" },
  { name: "Education", link: "#education" },
  { name: "Project", link: "#project" },
  { name: "Contact", link: "#contact" },
];

// Progress circle calculations
const circumference = 2 * Math.PI * 24; // radius = 24
const progressOffset = computed(() => {
  return circumference - (scrollProgress.value / 100) * circumference;
});

// Scroll event handler
const handleScroll = () => {
  const scrollTop = window.pageYOffset || document.documentElement.scrollTop;
  const windowHeight =
    document.documentElement.scrollHeight - window.innerHeight;

  // Show button after 300px scroll
  showScrollButton.value = scrollTop > 300;

  // Calculate scroll progress
  scrollProgress.value = (scrollTop / windowHeight) * 100;
};

// Smooth scroll to top
const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: "smooth",
  });
};

// Lifecycle hooks
onMounted(() => {
  window.addEventListener("scroll", handleScroll, { passive: true });
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>

<style scoped>
/* Scroll to Top Button Styles */
.scroll-to-top-btn {
  position: fixed;
  bottom: 30px;
  right: 30px;
  width: 56px;
  height: 56px;
  border: none;
  border-radius: 50%;
  cursor: pointer;
  z-index: 1000;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 8px 25px rgba(59, 130, 246, 0.3);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  backdrop-filter: blur(10px);
  overflow: hidden;
}

.scroll-to-top-btn:hover {
  transform: translateY(-3px) scale(1.05);
  box-shadow: 0 12px 35px rgba(59, 130, 246, 0.4);
}

.scroll-to-top-btn:active {
  transform: translateY(-1px) scale(0.98);
}

.scroll-btn-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, #3b82f6 0%, #1d4ed8 100%);
  border-radius: 50%;
  opacity: 0.9;
  transition: opacity 0.3s ease;
}

.scroll-to-top-btn:hover .scroll-btn-bg {
  opacity: 1;
}

.scroll-btn-icon {
  position: relative;
  z-index: 3;
  color: white;
  transition: transform 0.3s ease;
}

.scroll-to-top-btn:hover .scroll-btn-icon {
  transform: translateY(-2px);
}

.scroll-btn-progress {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 2;
}

.progress-ring {
  transform: rotate(-90deg);
  width: 100%;
  height: 100%;
}

.progress-ring-circle {
  fill: transparent;
  stroke: rgba(255, 255, 255, 0.3);
  stroke-width: 2;
  stroke-linecap: round;
  transition: stroke-dashoffset 0.1s linear;
}

/* Responsive positioning */
@media (max-width: 768px) {
  .scroll-to-top-btn {
    bottom: 20px;
    right: 20px;
    width: 50px;
    height: 50px;
  }

  .progress-ring {
    width: 50px;
    height: 50px;
  }

  .progress-ring-circle {
    cx: 25;
    cy: 25;
    r: 21;
  }
}

@media (max-width: 480px) {
  .scroll-to-top-btn {
    bottom: 16px;
    right: 16px;
    width: 48px;
    height: 48px;
  }

  .scroll-btn-icon {
    font-size: 18px;
  }
}

/* Transition animations */
.scroll-btn-enter-active,
.scroll-btn-leave-active {
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.scroll-btn-enter-from {
  opacity: 0;
  transform: translateY(20px) scale(0.8);
}

.scroll-btn-leave-to {
  opacity: 0;
  transform: translateY(20px) scale(0.8);
}

/* Pulse animation on first appearance */
@keyframes pulse-glow {
  0% {
    box-shadow: 0 8px 25px rgba(59, 130, 246, 0.3);
  }
  50% {
    box-shadow: 0 8px 35px rgba(59, 130, 246, 0.5);
  }
  100% {
    box-shadow: 0 8px 25px rgba(59, 130, 246, 0.3);
  }
}

.scroll-btn-visible {
  animation: pulse-glow 2s ease-in-out;
}

/* Accessibility improvements */
.scroll-to-top-btn:focus {
  outline: 2px solid #60a5fa;
  outline-offset: 2px;
}

.scroll-to-top-btn:focus:not(:focus-visible) {
  outline: none;
}

/* Reduced motion support */
@media (prefers-reduced-motion: reduce) {
  .scroll-to-top-btn,
  .scroll-btn-icon,
  .scroll-btn-bg,
  .progress-ring-circle {
    transition: none;
  }

  .scroll-btn-visible {
    animation: none;
  }

  .scroll-to-top-btn:hover {
    transform: none;
  }
}
</style>

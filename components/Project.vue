<template>
  <div class="projects-section py-16">
    <div class="container mx-auto px-4">
      <h1 class="text-center font-bold text-4xl mb-3 text-white">Projects</h1>
      <div class="w-24 h-1 bg-blue-500 mx-auto mb-6"></div>
      <p class="mt-5 text-center text-gray-300 max-w-2xl mx-auto mb-12">
        I have built my own projects to practice my front-end skills and also to
        understand how to communicate with back-end.
      </p>

      <!-- Projects Grid -->
      <div class="grid lg:grid-cols-3 md:grid-cols-2 sm:grid-cols-1 gap-8">
        <div
          v-for="(project, idx) in projects"
          :key="idx"
          class="project-card"
          @click="openProjectDetails(project)"
        >
          <!-- Image Carousel -->
          <div class="carousel-container relative overflow-hidden rounded-t-lg">
            <div
              class="carousel-inner flex transition-transform duration-500 ease-in-out h-48 md:h-56"
              :style="{
                transform: `translateX(-${currentSlides[idx] * 100}%)`,
              }"
            >
              <div
                v-for="(image, imageIdx) in project.images"
                :key="imageIdx"
                class="carousel-slide min-w-full h-full"
              >
                <NuxtImg
                  :src="image"
                  class="w-full h-full object-cover"
                  loading="lazy"
                />
              </div>
            </div>

            <!-- Carousel Controls -->
            <div
              class="carousel-controls absolute bottom-2 left-0 right-0 flex justify-center space-x-2"
            >
              <button
                v-for="(_, dotIdx) in project.images"
                :key="dotIdx"
                @click.stop="setSlide(idx, dotIdx)"
                :class="[
                  'carousel-dot',
                  currentSlides[idx] === dotIdx ? 'active' : '',
                ]"
              ></button>
            </div>

            <!-- Navigation Arrows -->
            <button
              @click.stop="prevSlide(idx, project.images.length)"
              class="carousel-arrow left-2"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                fill="currentColor"
                class="w-6 h-6"
              >
                <path
                  fill-rule="evenodd"
                  d="M7.72 12.53a.75.75 0 010-1.06l7.5-7.5a.75.75 0 111.06 1.06L9.31 12l6.97 6.97a.75.75 0 11-1.06 1.06l-7.5-7.5z"
                  clip-rule="evenodd"
                />
              </svg>
            </button>
            <button
              @click.stop="nextSlide(idx, project.images.length)"
              class="carousel-arrow right-2"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                fill="currentColor"
                class="w-6 h-6"
              >
                <path
                  fill-rule="evenodd"
                  d="M16.28 11.47a.75.75 0 010 1.06l-7.5 7.5a.75.75 0 01-1.06-1.06L14.69 12 7.72 5.03a.75.75 0 011.06-1.06l7.5 7.5z"
                  clip-rule="evenodd"
                />
              </svg>
            </button>
          </div>

          <!-- Project Info -->
          <div class="project-info p-6">
            <div class="flex justify-between items-start mb-3">
              <h2 class="font-bold text-xl text-white">{{ project.title }}</h2>
              <span class="text-blue-400 text-sm">{{ project.date }}</span>
            </div>

            <p class="text-gray-300 mb-4 line-clamp-3">{{ project.detail }}</p>

            <!-- Technologies -->
            <div class="flex flex-wrap gap-2 mb-4">
              <span
                v-for="(tech, techIdx) in project.languages"
                :key="techIdx"
                class="tech-badge"
              >
                {{ tech }}
              </span>
            </div>

            <!-- View Details Button -->
            <button class="view-details-btn">
              View Details
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
                fill="currentColor"
                class="w-5 h-5 ml-1"
              >
                <path
                  fill-rule="evenodd"
                  d="M3 10a.75.75 0 01.75-.75h10.638L10.23 5.29a.75.75 0 111.04-1.08l5.5 5.25a.75.75 0 010 1.08l-5.5 5.25a.75.75 0 11-1.04-1.08l4.158-3.96H3.75A.75.75 0 013 10z"
                  clip-rule="evenodd"
                />
              </svg>
            </button>
          </div>
        </div>
      </div>

      <!-- Project Details Modal -->
      <Teleport to="body">
        <div
          v-if="selectedProject"
          class="modal-backdrop"
          @click="closeProjectDetails"
        >
          <div class="modal-content" @click.stop>
            <!-- Modal Close Button -->
            <button class="modal-close" @click="closeProjectDetails">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
                fill="currentColor"
                class="w-6 h-6"
              >
                <path
                  fill-rule="evenodd"
                  d="M5.47 5.47a.75.75 0 011.06 0L12 10.94l5.47-5.47a.75.75 0 111.06 1.06L13.06 12l5.47 5.47a.75.75 0 11-1.06 1.06L12 13.06l-5.47 5.47a.75.75 0 01-1.06-1.06L10.94 12 5.47 6.53a.75.75 0 010-1.06z"
                  clip-rule="evenodd"
                />
              </svg>
            </button>

            <!-- Modal Content -->
            <div class="modal-header">
              <h2 class="text-2xl font-bold text-white">
                {{ selectedProject.title }}
              </h2>
              <span class="text-blue-400">{{ selectedProject.date }}</span>
            </div>

            <!-- Full Image Carousel -->
            <div
              class="modal-carousel relative overflow-hidden rounded-lg my-6"
            >
              <div
                class="carousel-inner flex transition-transform duration-500 ease-in-out h-64 md:h-96"
                :style="{
                  transform: `translateX(-${modalCurrentSlide * 100}%)`,
                }"
              >
                <div
                  v-for="(image, imageIdx) in selectedProject.images"
                  :key="imageIdx"
                  class="carousel-slide min-w-full h-full"
                >
                  <NuxtImg
                    :src="image"
                    class="w-full h-full object-contain bg-gray-900"
                    loading="lazy"
                  />
                </div>
              </div>

              <!-- Modal Carousel Controls -->
              <div
                class="carousel-controls absolute bottom-4 left-0 right-0 flex justify-center space-x-3"
              >
                <button
                  v-for="(_, dotIdx) in selectedProject.images"
                  :key="dotIdx"
                  @click="modalCurrentSlide = dotIdx"
                  :class="[
                    'carousel-dot',
                    modalCurrentSlide === dotIdx ? 'active' : '',
                  ]"
                ></button>
              </div>

              <!-- Modal Navigation Arrows -->
              <button
                @click="prevModalSlide(selectedProject.images.length)"
                class="carousel-arrow left-4"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 24 24"
                  fill="currentColor"
                  class="w-8 h-8"
                >
                  <path
                    fill-rule="evenodd"
                    d="M7.72 12.53a.75.75 0 010-1.06l7.5-7.5a.75.75 0 111.06 1.06L9.31 12l6.97 6.97a.75.75 0 11-1.06 1.06l-7.5-7.5z"
                    clip-rule="evenodd"
                  />
                </svg>
              </button>
              <button
                @click="nextModalSlide(selectedProject.images.length)"
                class="carousel-arrow right-4"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 24 24"
                  fill="currentColor"
                  class="w-8 h-8"
                >
                  <path
                    fill-rule="evenodd"
                    d="M16.28 11.47a.75.75 0 010 1.06l-7.5 7.5a.75.75 0 01-1.06-1.06L14.69 12 7.72 5.03a.75.75 0 011.06-1.06l7.5 7.5z"
                    clip-rule="evenodd"
                  />
                </svg>
              </button>
            </div>

            <!-- Project Details -->
            <div class="modal-body">
              <p class="text-gray-300 mb-6">{{ selectedProject.detail }}</p>

              <!-- Features List -->
              <div class="mb-6">
                <h3 class="text-xl font-semibold text-white mb-3">
                  Key Features
                </h3>
                <ul class="features-list">
                  <li
                    v-for="(feature, featureIdx) in selectedProject.features"
                    :key="featureIdx"
                  >
                    {{ feature }}
                  </li>
                </ul>
              </div>

              <!-- Technologies Used -->
              <div class="mb-6">
                <h3 class="text-xl font-semibold text-white mb-3">
                  Technologies Used
                </h3>
                <div class="flex flex-wrap gap-2">
                  <span
                    v-for="(tech, techIdx) in selectedProject.languages"
                    :key="techIdx"
                    class="tech-badge-large"
                  >
                    {{ tech }}
                  </span>
                </div>
              </div>

              <!-- Project Links -->
              <div class="flex gap-4 mt-8">
                <a
                  v-if="selectedProject.demo"
                  :href="selectedProject.demo"
                  target="_blank"
                  class="project-link demo-link"
                >
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 24 24"
                    fill="currentColor"
                    class="w-5 h-5 mr-2"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M2.25 12c0-5.385 4.365-9.75 9.75-9.75s9.75 4.365 9.75 9.75-4.365 9.75-9.75 9.75S2.25 17.385 2.25 12zm14.024-.983a1.125 1.125 0 010 1.966l-5.603 3.113A1.125 1.125 0 019 15.113V8.887c0-.857.921-1.4 1.671-.983l5.603 3.113z"
                      clip-rule="evenodd"
                    />
                  </svg>
                  View Demo
                </a>
                <a
                  :href="selectedProject.source"
                  target="_blank"
                  class="project-link source-link"
                >
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 24 24"
                    fill="currentColor"
                    class="w-5 h-5 mr-2"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M14.447 3.027a.75.75 0 01.527.92l-4.5 16.5a.75.75 0 01-1.448-.394l4.5-16.5a.75.75 0 01.921-.526zM16.72 6.22a.75.75 0 011.06 0l5.25 5.25a.75.75 0 010 1.06l-5.25 5.25a.75.75 0 11-1.06-1.06L21.44 12l-4.72-4.72a.75.75 0 010-1.06zm-9.44 0a.75.75 0 010 1.06L2.56 12l4.72 4.72a.75.75 0 11-1.06 1.06L.97 12.53a.75.75 0 010-1.06l5.25-5.25a.75.75 0 011.06 0z"
                      clip-rule="evenodd"
                    />
                  </svg>
                  View Source
                </a>
              </div>
            </div>
          </div>
        </div>
      </Teleport>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const { projects } = await import("~/data.json");

// Carousel state for each project card
const currentSlides = ref(projects.map(() => 0));

// Set up carousel functions
function nextSlide(projectIndex, totalSlides) {
  currentSlides.value[projectIndex] =
    (currentSlides.value[projectIndex] + 1) % totalSlides;
}

function prevSlide(projectIndex, totalSlides) {
  currentSlides.value[projectIndex] =
    (currentSlides.value[projectIndex] - 1 + totalSlides) % totalSlides;
}

function setSlide(projectIndex, slideIndex) {
  currentSlides.value[projectIndex] = slideIndex;
}

// Modal state and functions
const selectedProject = ref(null);
const modalCurrentSlide = ref(0);

function openProjectDetails(project) {
  selectedProject.value = project;
  modalCurrentSlide.value = 0;
  document.body.style.overflow = "hidden"; // Prevent scrolling when modal is open
}

function closeProjectDetails() {
  selectedProject.value = null;
  document.body.style.overflow = ""; // Restore scrolling
}

function nextModalSlide(totalSlides) {
  modalCurrentSlide.value = (modalCurrentSlide.value + 1) % totalSlides;
}

function prevModalSlide(totalSlides) {
  modalCurrentSlide.value =
    (modalCurrentSlide.value - 1 + totalSlides) % totalSlides;
}
</script>

<style scoped>
.projects-section {
  background: linear-gradient(135deg, #0f172a 0%, #1e3a8a 100%);
}

.project-card {
  background: rgba(15, 23, 42, 0.8);
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  cursor: pointer;
  border: 1px solid rgba(59, 130, 246, 0.2);
  backdrop-filter: blur(10px);
}

.project-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.3);
  border-color: rgba(59, 130, 246, 0.5);
}

.carousel-arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(0, 0, 0, 0.5);
  color: white;
  border-radius: 50%;
  width: 36px;
  height: 36px;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
  opacity: 0.7;
  transition: opacity 0.2s ease;
}

.carousel-arrow:hover {
  opacity: 1;
}

.carousel-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.5);
  transition: all 0.3s ease;
}

.carousel-dot.active {
  background: #3b82f6;
  transform: scale(1.2);
}

.tech-badge {
  padding: 0.25rem 0.75rem;
  background: rgba(59, 130, 246, 0.15);
  color: #93c5fd;
  border-radius: 20px;
  font-size: 0.75rem;
  font-weight: 500;
  border: 1px solid rgba(59, 130, 246, 0.3);
}

.tech-badge-large {
  padding: 0.5rem 1rem;
  background: rgba(59, 130, 246, 0.15);
  color: #93c5fd;
  border-radius: 20px;
  font-size: 0.875rem;
  font-weight: 500;
  border: 1px solid rgba(59, 130, 246, 0.3);
}

.view-details-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0.5rem 1rem;
  background: rgba(59, 130, 246, 0.15);
  color: #60a5fa;
  border-radius: 6px;
  font-weight: 500;
  transition: all 0.3s ease;
  border: 1px solid rgba(59, 130, 246, 0.3);
  width: 100%;
}

.view-details-btn:hover {
  background: rgba(59, 130, 246, 0.25);
  border-color: rgba(59, 130, 246, 0.5);
}

/* Modal Styles */
.modal-backdrop {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 50;
  padding: 1rem;
  backdrop-filter: blur(5px);
}

.modal-content {
  background: rgba(15, 23, 42, 0.95);
  border-radius: 12px;
  width: 100%;
  max-width: 900px;
  max-height: 90vh;
  overflow-y: auto;
  position: relative;
  border: 1px solid rgba(59, 130, 246, 0.3);
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.25);
}

.modal-close {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: rgba(0, 0, 0, 0.5);
  color: white;
  border-radius: 50%;
  width: 36px;
  height: 36px;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
  transition: all 0.2s ease;
}

.modal-close:hover {
  background: rgba(239, 68, 68, 0.8);
  transform: rotate(90deg);
}

.modal-header {
  padding: 1.5rem 2rem;
  border-bottom: 1px solid rgba(59, 130, 246, 0.2);
}

.modal-body {
  padding: 1.5rem 2rem 2rem;
}

.features-list {
  list-style-type: none;
  padding-left: 0;
}

.features-list li {
  position: relative;
  padding-left: 1.5rem;
  margin-bottom: 0.75rem;
  color: #d1d5db;
}

.features-list li::before {
  content: "";
  position: absolute;
  left: 0;
  top: 0.5rem;
  width: 0.5rem;
  height: 0.5rem;
  border-radius: 50%;
  background: #3b82f6;
}

.project-link {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0.75rem 1.5rem;
  border-radius: 8px;
  font-weight: 600;
  transition: all 0.3s ease;
}

.demo-link {
  background: #3b82f6;
  color: white;
}

.demo-link:hover {
  background: #2563eb;
  transform: translateY(-2px);
}

.source-link {
  background: transparent;
  color: white;
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.source-link:hover {
  background: rgba(255, 255, 255, 0.1);
  transform: translateY(-2px);
}

/* Custom scrollbar for modal */
.modal-content::-webkit-scrollbar {
  width: 8px;
}

.modal-content::-webkit-scrollbar-track {
  background: rgba(15, 23, 42, 0.5);
}

.modal-content::-webkit-scrollbar-thumb {
  background: rgba(59, 130, 246, 0.5);
  border-radius: 4px;
}

.modal-content::-webkit-scrollbar-thumb:hover {
  background: rgba(59, 130, 246, 0.7);
}
</style>

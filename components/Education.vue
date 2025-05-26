<template>
  <div class="education-container py-16">
    <div class="container mx-auto px-4">
      <div class="section-header mb-12">
        <h1 class="text-center font-bold text-4xl mb-3 text-white">
          Education
        </h1>
        <div class="w-24 h-1 bg-blue-500 mx-auto mb-6"></div>
        <p class="text-center text-gray-300 max-w-2xl mx-auto">
          My education has been about more than academic learning, it has also
          been about understanding myself and experiencing personal growth.
        </p>
      </div>

      <div class="timeline-container">
        <div class="timeline-line"></div>

        <div
          v-for="(edu, i) in education"
          :key="i"
          class="timeline-item"
          :class="i % 2 === 0 ? 'left' : 'right'"
        >
          <div class="timeline-dot">
            <div class="dot-inner"></div>
          </div>

          <div class="timeline-content">
            <div class="education-card">
              <div class="education-header">
                <div class="education-image">
                  <NuxtImg
                    :src="edu.image"
                    class="rounded-full object-cover"
                    width="80"
                    height="80"
                  />
                </div>
                <div class="education-title">
                  <h2 class="text-xl font-bold text-white">{{ edu.name }}</h2>
                  <div class="education-date">
                    <Icon name="mdi:calendar-clock" class="mr-1" />
                    <span>{{ edu.date }}</span>
                  </div>
                </div>
              </div>

              <div 
                class="education-body"
                :class="{ 'expanded': expandedItems.includes(i) }"
              >
                <p>{{ edu.detail }}</p>
              </div>

              <div class="education-footer">
                <button 
                  class="read-more-btn" 
                  @click="toggleReadMore(i)"
                  :class="{ 'active': expandedItems.includes(i) }"
                >
                  {{ expandedItems.includes(i) ? "Read Less" : "Read More" }}
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const { education } = await import("~/data.json");
const expandedItems = ref([]);

function toggleReadMore(index) {
  if (expandedItems.value.includes(index)) {
    expandedItems.value = expandedItems.value.filter((i) => i !== index);
  } else {
    expandedItems.value.push(index);
  }
}
</script>

<style scoped>
.education-container {
  background: linear-gradient(135deg, #0f172a 0%, #1e3a8a 100%);
  position: relative;
  overflow: hidden;
  min-height: 100vh;
}

.education-container::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(
    circle at 20% 50%,
    rgba(59, 130, 246, 0.1) 0%,
    transparent 50%
  );
  pointer-events: none;
}

.timeline-container {
  position: relative;
  max-width: 1200px;
  margin: 0 auto;
  padding: 40px 0;
}

.timeline-line {
  position: absolute;
  width: 4px;
  background: linear-gradient(180deg, #3b82f6 0%, #1e40af 100%);
  top: 0;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  border-radius: 2px;
  box-shadow: 0 0 10px rgba(59, 130, 246, 0.3);
}

.timeline-item {
  position: relative;
  margin-bottom: 60px;
  width: 50%;
  opacity: 0;
  animation: fadeInUp 0.6s ease forwards;
}

.timeline-item:nth-child(2n) { animation-delay: 0.1s; }
.timeline-item:nth-child(3n) { animation-delay: 0.2s; }
.timeline-item:nth-child(4n) { animation-delay: 0.3s; }

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.timeline-item.left {
  left: 0;
  padding-right: 40px;
}

.timeline-item.right {
  left: 50%;
  padding-left: 40px;
}

.timeline-dot {
  position: absolute;
  width: 20px;
  height: 20px;
  background: linear-gradient(135deg, #3b82f6 0%, #1e40af 100%);
  border-radius: 50%;
  top: 20px;
  border: 3px solid #60a5fa;
  z-index: 2;
  transition: all 0.3s ease;
  box-shadow: 0 0 20px rgba(59, 130, 246, 0.4);
}

.timeline-item:hover .timeline-dot {
  transform: scale(1.2);
  box-shadow: 0 0 25px rgba(59, 130, 246, 0.6);
}

.timeline-item.left .timeline-dot {
  right: -10px;
}

.timeline-item.right .timeline-dot {
  left: -10px;
}

.dot-inner {
  position: absolute;
  width: 8px;
  height: 8px;
  background-color: #60a5fa;
  border-radius: 50%;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0% {
    transform: translate(-50%, -50%) scale(1);
    opacity: 1;
  }
  50% {
    transform: translate(-50%, -50%) scale(1.3);
    opacity: 0.7;
  }
  100% {
    transform: translate(-50%, -50%) scale(1);
    opacity: 1;
  }
}

.timeline-content {
  position: relative;
}

.education-card {
  background: rgba(15, 23, 42, 0.9);
  border-radius: 16px;
  border: 1px solid rgba(59, 130, 246, 0.3);
  padding: 24px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
  backdrop-filter: blur(12px);
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  overflow: hidden;
}

.education-card::before {
  content: "";
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(59, 130, 246, 0.1),
    transparent
  );
  transition: left 0.5s ease;
}

.education-card:hover::before {
  left: 100%;
}

.education-card:hover {
  transform: translateY(-8px) scale(1.02);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
  border-color: rgba(59, 130, 246, 0.6);
}

.education-header {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
  position: relative;
  z-index: 1;
}

.education-image {
  margin-right: 20px;
  position: relative;
  flex-shrink: 0;
}

.education-image img {
  border: 3px solid rgba(59, 130, 246, 0.4);
  transition: all 0.3s ease;
}

.education-card:hover .education-image img {
  border-color: rgba(59, 130, 246, 0.8);
  box-shadow: 0 0 20px rgba(59, 130, 246, 0.4);
}

.education-image::after {
  content: "";
  position: absolute;
  top: -5px;
  left: -5px;
  right: -5px;
  bottom: -5px;
  border-radius: 50%;
  border: 2px solid rgba(59, 130, 246, 0.3);
  animation: rotate 15s linear infinite;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.education-card:hover .education-image::after {
  opacity: 1;
}

@keyframes rotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.education-title {
  flex: 1;
  min-width: 0;
}

.education-title h2 {
  margin-bottom: 8px;
  transition: color 0.3s ease;
}

.education-card:hover .education-title h2 {
  color: #60a5fa;
}

.education-date {
  display: flex;
  align-items: center;
  color: #60a5fa;
  font-size: 0.9rem;
  font-weight: 500;
  transition: color 0.3s ease;
}

.education-card:hover .education-date {
  color: #93c5fd;
}

.education-body {
  color: #cbd5e1;
  line-height: 1.7;
  position: relative;
  z-index: 1;
  transition: all 0.4s ease;
  max-height: 3.4em; /* About 2 lines */
  overflow: hidden;
  position: relative;
}

.education-body:not(.expanded)::after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 1.5em;
  background: linear-gradient(transparent, rgba(15, 23, 42, 0.9));
  pointer-events: none;
}

.education-body.expanded {
  max-height: none;
}

.education-body.expanded::after {
  display: none;
}

.education-footer {
  margin-top: 20px;
  text-align: right;
  position: relative;
  z-index: 1;
}

.read-more-btn {
  background: linear-gradient(135deg, #3b82f6 0%, #1e40af 100%);
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 20px;
  cursor: pointer;
  font-weight: 600;
  font-size: 0.9rem;
  transition: all 0.3s ease;
  box-shadow: 0 4px 12px rgba(59, 130, 246, 0.3);
  position: relative;
  overflow: hidden;
}

.read-more-btn::before {
  content: "";
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: left 0.5s ease;
}

.read-more-btn:hover::before {
  left: 100%;
}

.read-more-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(59, 130, 246, 0.4);
  background: linear-gradient(135deg, #60a5fa 0%, #3b82f6 100%);
}

.read-more-btn:active {
  transform: translateY(0);
}

.read-more-btn.active {
  background: linear-gradient(135deg, #ef4444 0%, #dc2626 100%);
  box-shadow: 0 4px 12px rgba(239, 68, 68, 0.3);
}

.read-more-btn.active:hover {
  background: linear-gradient(135deg, #f87171 0%, #ef4444 100%);
  box-shadow: 0 6px 16px rgba(239, 68, 68, 0.4);
}

/* Mobile Responsiveness */
@media (max-width: 768px) {
  .timeline-line {
    left: 30px;
  }

  .timeline-item {
    width: 100%;
    padding-left: 70px;
    padding-right: 20px;
    margin-bottom: 40px;
  }

  .timeline-item.left,
  .timeline-item.right {
    left: 0;
    padding-left: 70px;
    padding-right: 20px;
  }

  .timeline-item.left .timeline-dot,
  .timeline-item.right .timeline-dot {
    left: 20px;
    right: auto;
  }

  .education-card {
    padding: 20px;
  }

  .education-header {
    flex-direction: column;
    text-align: center;
    margin-bottom: 16px;
  }

  .education-image {
    margin-right: 0;
    margin-bottom: 12px;
  }

  .education-body {
    font-size: 0.9rem;
  }

  .education-footer {
    text-align: center;
    margin-top: 16px;
  }
}

@media (max-width: 480px) {
  .education-container {
    padding: 40px 0;
  }

  .section-header h1 {
    font-size: 2.5rem;
  }

  .timeline-item {
    padding-left: 60px;
  }

  .timeline-item.left .timeline-dot,
  .timeline-item.right .timeline-dot {
    left: 15px;
  }

  .timeline-line {
    left: 25px;
  }
}
</style>
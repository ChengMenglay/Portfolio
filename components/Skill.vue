<template>
  <div class="skills-container py-16">
    <section class="container mx-auto px-4">
      <div class="section-header mb-12">
        <h1 class="text-center font-bold text-4xl mb-3 text-white">Skills</h1>
        <div class="w-24 h-1 bg-blue-500 mx-auto mb-6"></div>
        <p class="text-center text-gray-300 max-w-2xl mx-auto">
          Here are some of my technical skills that I have been developing
          through various courses and projects.
        </p>
      </div>

      <div class="unified-skill-card">
        <div class="skill-categories mb-8">
          <button 
            v-for="category in ['All', 'Frontend', 'Backend', 'Tools']" 
            :key="category"
            @click="activeCategory = category"
            :class="['category-btn', activeCategory === category ? 'active' : '']"
          >
            {{ category }}
          </button>
        </div>

        <div class="skill-grid">
          <!-- Frontend Skills -->
          <div 
            v-for="(skill, i) in filteredSkills" 
            :key="i"
            class="skill-item"
            :class="getSkillClass(skill.category)"
          >
            <div class="skill-icon" :class="getIconClass(skill.category)">
              <Icon :name="skill.icon" />
            </div>
            <div class="skill-info">
              <div class="flex justify-between mb-1">
                <p class="skill-name">{{ skill.name }}</p>
                <span class="text-xs" :class="getTextClass(skill.category)">
                  {{ skill.proficiency }}%
                </span>
              </div>
              <div class="skill-bar">
                <div
                  class="skill-progress"
                  :class="skill.category.toLowerCase()"
                  :style="{ width: skill.proficiency + '%' }"
                ></div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const { skill } = await import("~/data.json");
const activeCategory = ref('All');

// Combine all skills into a single array with category information
const allSkills = [
  ...skill.fronted.map(item => ({ ...item, category: 'Frontend' })),
  ...skill.backend.map(item => ({ ...item, category: 'Backend' })),
  ...skill.tool.map(item => ({ ...item, category: 'Tools' }))
];

// Filter skills based on active category
const filteredSkills = computed(() => {
  if (activeCategory.value === 'All') {
    return allSkills;
  }
  return allSkills.filter(skill => skill.category === activeCategory.value);
});

// Helper functions for styling
function getSkillClass(category) {
  return {
    'frontend-item': category === 'Frontend',
    'backend-item': category === 'Backend',
    'tool-item': category === 'Tools'
  };
}

function getIconClass(category) {
  return {
    'frontend-icon': category === 'Frontend',
    'backend-icon': category === 'Backend',
    'tool-icon': category === 'Tools'
  };
}

function getTextClass(category) {
  return {
    'text-blue-300': category === 'Frontend',
    'text-green-300': category === 'Backend',
    'text-red-300': category === 'Tools'
  };
}
</script>

<style scoped>
.skills-container {
  background: linear-gradient(135deg, #0f172a 0%, #1e3a8a 100%);
  position: relative;
  overflow: hidden;
}

.skills-container::before {
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
}

.unified-skill-card {
  background: rgba(15, 23, 42, 0.8);
  border-radius: 12px;
  border: 1px solid rgba(59, 130, 246, 0.3);
  padding: 2rem;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
  backdrop-filter: blur(10px);
}

.skill-categories {
  display: flex;
  justify-content: center;
  gap: 1rem;
  flex-wrap: wrap;
}

.category-btn {
  padding: 0.5rem 1.5rem;
  border-radius: 30px;
  background: rgba(30, 41, 59, 0.5);
  color: white;
  font-weight: 600;
  transition: all 0.3s ease;
  border: 1px solid transparent;
}

.category-btn:hover {
  background: rgba(30, 41, 59, 0.8);
  transform: translateY(-2px);
}

.category-btn.active {
  background: #3b82f6;
  box-shadow: 0 4px 12px rgba(59, 130, 246, 0.3);
}

.skill-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1.5rem;
  margin-top: 2rem;
}

.skill-item {
  display: flex;
  align-items: center;
  padding: 1rem;
  border-radius: 8px;
  background: rgba(30, 41, 59, 0.5);
  transition: all 0.3s ease;
  border-left: 3px solid transparent;
}

.skill-item:hover {
  background: rgba(30, 41, 59, 0.8);
  transform: translateX(5px);
}

.frontend-item {
  border-left-color: #3b82f6;
}

.backend-item {
  border-left-color: #10b981;
}

.tool-item {
  border-left-color: #f43f5e;
}

.skill-icon {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 3rem;
  height: 3rem;
  font-size: 2rem;
  margin-right: 1rem;
}

.frontend-icon {
  color: #3b82f6;
}

.backend-icon {
  color: #10b981;
}

.tool-icon {
  color: #f43f5e;
}

.skill-info {
  flex: 1;
}

.skill-name {
  font-weight: 600;
  color: white;
}

.skill-bar {
  height: 6px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 3px;
  overflow: hidden;
}

.skill-progress {
  height: 100%;
  border-radius: 3px;
  transition: width 1.5s ease-out;
}

.frontend {
  background: linear-gradient(90deg, #3b82f6, #60a5fa);
}

.backend {
  background: linear-gradient(90deg, #10b981, #34d399);
}

.tools {
  background: linear-gradient(90deg, #f43f5e, #fb7185);
}

@media (max-width: 768px) {
  .skill-grid {
    grid-template-columns: 1fr;
  }
}
</style>
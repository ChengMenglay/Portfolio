<template>
  <div>
    <h1 class="text-center font-bold text-4xl">Projects</h1>
    <p class="mt-5 text-center text-gray-400">
      I have built my own projects to practice my front-end skills and also to
      understand how to communicate with back-end.
    </p>
    <div
      class="grid lg:grid-cols-3 md:grid-cols-2 sm:grid-cols-2 grid-cols-1 gap-5 mt-10 px-3"
    >
      <div
        class="p-7 bg-sky-950 rounded-lg relative hover:-translate-y-3 duration-300"
        v-for="(project, idx) in projects"
        :key="idx"
      >
        <!-- <NuxtImg src="../public/pos.webp" /> -->

        <NuxtImg
          :src="project.image"
          quality="80"
          class="h-[30%] mx-auto w-full"
        />
        <div class="flex justify-center mt-5 flex-wrap gap-2 max-h-[20%]">
          <p
            class="w-20 flex justify-center items-center h-8 rounded-md border border-blue-600 text-blue-400"
            v-for="(p, idx) in project.languages"
            :key="idx"
          >
            {{ p }}
          </p>
        </div>
        <div class="max-h-[15%]">
          <h1 class="font-bold text-2xl mt-2">{{ project.title }}</h1>
          <span class="text-gray-500 text-sm">{{ project.date }}</span>
        </div>

        <div
          class="max-h-[20%] overflow-hidden overflow-ellipsis line-clamp-3 hover:line-clamp-none duration-300"
        >
          <p class="text-gray-400">
            {{ project.detail }}
          </p>
        </div>
        <div class="flex gap-5 absolute bottom-3">
          <NuxtLink
            class="px-5 py-2 bg-blue-700 border border-blue-500 rounded-lg text-white hover:bg-blue-800 duration-300"
            target="_blank"
            :to="project.demo"
            >Demo</NuxtLink
          >
          <NuxtLink
            class="px-5 py-2 border border-blue-500 rounded-lg text-white hover:bg-blue-800 duration-300"
            :to="project.source"
            target="_blank"
            >Source</NuxtLink
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const { projects } = await import("~/data.json");
</script>

<style scoped></style>

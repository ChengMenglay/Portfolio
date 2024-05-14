<template>
  <div>
    <h1 class="text-center font-bold text-4xl">Education</h1>
    <p class="text-center text-gray-400 mt-5">
      My Education has been about more than academic learning, it has also
      understanding myself and experiencing personal growth.
    </p>
    <p class="text-center text-gray-400">
      Here are the details of my education.
    </p>
    <div class="max-w-[850px] mx-auto grid grid-cols-1 gap-10 mt-10">
      <div
        class="px-10 mx-3 py-7 border border-blue-800 rounded-md hover:-translate-y-3 duration-300"
        v-for="(edu, i) in education"
        :key="i"
      >
        <div class="flex items-center gap-5">
          <NuxtImg
            :src="edu.image"
            class="w-14 h-14 rounded-full object-cover"
          ></NuxtImg>
          <div>
            <h1>{{ edu.name }}</h1>
            <p class="text-gray-500">{{ edu.date }}</p>
          </div>
        </div>
        <div
          class="line-clamp-3 lg:px-[75px] md:px-[75px] hover:line-clamp-none duration-300"
        >
          <p class="text-gray-400 mt-5">
            {{ edu.detail }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const { education } = await import("~/data.json");
</script>

<style scoped></style>

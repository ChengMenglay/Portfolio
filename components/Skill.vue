<template>
  <div>
    <section class="px-3">
      <h1 class="text-center font-bold text-4xl">Skills</h1>
      <div class="my-5">
        <p class="text-center text-gray-400">
          Here are some of my technical skill on which I have been learning via
          other courses.
        </p>
        <div
          class="mx-auto mt-20 grid lg:grid-cols-2 md:grid-cols-2 sm:grid-cols-1 gap-5"
        >
          <div
            class="border h-auto border-blue-800 bg-sky-950 shadow-sm px-3 py-2 shadow-blue-900"
          >
            <h1 class="text-center font-bold text-xl">Frontend</h1>
            <div
              class="flex justify-center mx-auto flex-wrap gap-3 mt-5 py-3 font-bold text-white"
            >
              <p
                class="border border-blue-900 flex justify-center items-center gap-3 px-5 py-5"
                v-for="(front, i) in skill.fronted"
                :key="i"
              >
                <Icon :name="front.icon" class="text-5xl" />
                {{ front.name }}
              </p>
            </div>
          </div>
          <div
            class="border min-h-[300px] border-blue-800 bg-sky-950 shadow-sm px-3 py-3 shadow-blue-900"
          >
            <h1 class="text-center font-bold text-xl">Backend</h1>
            <div
              class="flex justify-center flex-wrap gap-3 mt-5 font-bold text-white"
            >
              <p
                class="px-5 py-5 border border-blue-900 flex justify-center items-center gap-3"
                v-for="(back, i) in skill.backend"
                :key="i"
              >
                <Icon :name="back.icon" class="text-5xl" />
                {{ back.name }}
              </p>
            </div>
          </div>
          <div
            class="border min-h-[350px] border-blue-800 bg-sky-950 shadow-sm px-3 py-3 shadow-blue-900"
          >
            <h1 class="text-center font-bold text-xl">Tool</h1>
            <div
              class="flex justify-center flex-wrap gap-3 mt-5 font-bold text-white"
            >
              <p
                class="px-5 py-5 border border-blue-900 flex justify-center items-center gap-3"
                v-for="(tool, i) in skill.tool"
                :key="i"
              >
                <Icon :name="tool.icon" class="text-5xl text-red-600" />
                {{ tool.name }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
const { skill } = await import("~/data.json");
</script>

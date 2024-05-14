<template>
  <div
    class="grid lg:grid-cols-2 md:grid-cols-2 sm:grid-cols-1 h-[500px] mb-10 mx-3"
  >
    <div
      class="w-full rounded-s-lg flex flex-col justify-center items-center bg-blue-950"
    >
      <h1 class="text-6xl font-bold">Contact Me</h1>
      <p class="mt-5 text-xl">Feel free to reach out!</p>
    </div>
    <div
      class="w-full rounded-e-lg flex flex-col justify-center gap-10 px-5 bg-sky-950"
    >
      <p class="flex text-lg items-center gap-5">
        <Icon name="ic:sharp-mail" class="text-4xl" />cheng.menglay79@gmail.com
      </p>
      <p class="flex text-lg items-center gap-5">
        <Icon name="devicon:linkedin" class="text-4xl" /><NuxtLink
          to="https://bit.ly/chengmenglay"
          target="_blank"
          >https://bit.ly/chengmenglay</NuxtLink
        >
      </p>
      <p class="flex text-lg items-center gap-5">
        <Icon name="uiw:github" class="text-4xl" /><NuxtLink
          to="https://github.com/ChengMenglay"
          target="_blank"
          >https://github.com/ChengMenglay</NuxtLink
        >
      </p>
    </div>
  </div>
</template>

<script setup></script>

<style lang="scss" scoped></style>

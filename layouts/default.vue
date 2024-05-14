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
        ©2024 Cheng Menglay. All rights reserved.
      </p>
      <NuxtLink
        to="#home"
        class="p-1 absolute text-4xl lg:right-20 md:right-14 sm:right-7 right-7 lg:top-20 md:top-14 sm:top-7 top-7 flex justify-center items-center border border-blue-500 hover:-translate-y-3 hover:bg-blue-500 duration-300 rounded-full"
        ><Icon name="material-symbols:arrow-drop-up"></Icon
      ></NuxtLink>
    </footer>
  </div>
</template>

<script setup>
const nav = ref(false);
const links = [
  { name: "Home", link: "#home" },
  { name: "Skill", link: "#skill" },
  { name: "Education", link: "#education" },
  { name: "Project", link: "#project" },
  { name: "Contact", link: "#contact" },
];
</script>

<style scoped></style>

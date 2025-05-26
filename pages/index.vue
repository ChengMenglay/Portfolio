<template>
  <div class="scroll-smooth">
    <div id="home">
      <main class="lg:mt-48 md:mt-48 sm:mt-36 mt-36">
        <div
          class="lg:flex md:flex sm:block block justify-around items-center px-10"
        >
          <div class="lg:w-[50%] md:w-[50%] sm:w-[100%] w-[100%]">
            <h1 class="font-bold text-5xl">Hi, I am</h1>
            <h1 class="font-bold text-5xl">Cheng Menglay</h1>
            <h3 class="mt-3 font-bold text-2xl mb-6">
              I am a
              <span class="text-blue-500">Senior Student</span>
              <p>
                at Royal University of Phnom Penh majoring in Information
                Technology Engineering
              </p>
            </h3>
            <NuxtLink
              href="https://drive.google.com/file/d/1FjWfOzmkYO7mX5Ao7nkkdgNioeCmQwzp/view?usp=sharing"
              target="_blank"
              class="px-3 py-2 rounded-md border border-blue-600 text-blue-400 hover:bg-blue-600 hover:text-white duration-300"
              >View Resume</NuxtLink
            >
          </div>
          <NuxtImg
            src="/menglayy.jpg"
            class="lg:w-[300px] md:w-[300px] sm:w-[100%] mt-10 mx-auto rounded-lg"
            alt="portfolio_photo"
            quality="80"
          />
        </div>
      </main>
    </div>

    <div class="mt-40" id="skill">
      <Skill />
    </div>
    <div class="mt-40" id="education">
      <Education />
    </div>
    <div class="mt-40" id="project">
      <Project />
    </div>
    <div class="mt-40" id="contact">
      <Contact />
    </div>
  </div>
</template>

<script setup></script>

<style scoped></style>

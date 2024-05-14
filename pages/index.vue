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
            <h3 class="mt-3 font-bold text-2xl">
              I am a
              <span class="text-blue-500">Sophomore</span>
              <p>at RUPP majoring in Information Technology Engineering</p>
            </h3>
            <p class="text-md my-7">
              I am passionate in frontend developer with a solid foundation in
              HTML CSS and Javascript, always eager to take on new challanges
              and stay improving my technical skills via self-learning. My
              hobbies are coding and problem solving with relished.
            </p>
            <NuxtLink
              href="https://drive.google.com/file/d/1cse3X9ZbBWw-JFhB7mbkrnTNMXPulrQV/view?usp=drive_link"
              target="_blank"
              class="px-3 py-2 rounded-md border border-blue-600 text-blue-400 hover:bg-blue-600 hover:text-blue-300 duration-300"
              >View Resume</NuxtLink
            >
          </div>
          <NuxtImg
            src="/menglay.webp"
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

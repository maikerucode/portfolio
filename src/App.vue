<script setup>
  import HelloWorld from './components/HelloWorld.vue'
  import { ref, computed } from 'vue'
  import HomeSection from './sections/HomeSection.vue'
  import AboutSection from './sections/AboutSection.vue'
  import ProjectSection from './sections/ProjectSection.vue'
  import ContactSection from './sections/ContactSection.vue'
  import linkedin_logo from './assets/icons8-linkedin-100.png'

  const links = ['Home', 'About', 'Projects', 'Contact'];
  const active_index = ref(0);

  const sectionMap = [HomeSection, AboutSection, ProjectSection, ContactSection]
  const currentSection = computed(() => sectionMap[active_index.value])

  const menu_state = ref(0);
  const hamburger_state = ref(0);

  function toggleActive(index) {
    active_index.value = index;
    console.log("Clicked index: ", index);
  }

  function toggleMenu() {
    menu_state.value = !menu_state.value;
    console.log("Menu state: ", menu_state.value);
  }

  function toggleHamburger() {
    hamburger_state.value = !hamburger_state.value;
    console.log("Hamburger state: ", hamburger_state.value);
  }

  // console.log(active_index);
</script>

<template>
  <nav class="bg-gray-800">
  <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
    <div class="relative flex h-16 items-center justify-between">
      <div class="absolute inset-y-0 left-0 flex items-center sm:hidden">
        <!-- Mobile menu button-->
        <button @click.prevent="toggleHamburger" type="button" class="relative inline-flex items-center justify-center rounded-md p-2 text-gray-400 hover:bg-gray-700 hover:text-white focus:ring-2 focus:ring-white focus:outline-hidden focus:ring-inset" aria-controls="mobile-menu" aria-expanded="false">
          <span class="absolute -inset-0.5"></span>
          <span class="sr-only">Open main menu</span>
    
          <svg class="hidden size-6" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true" data-slot="icon">
            <path stroke-linecap="round" stroke-linejoin="round" d="M6 18 18 6M6 6l12 12" />
          </svg>

          <svg class="block size-6" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true" data-slot="icon">
            <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" />
          </svg>

        </button>
      </div>
      <div class="flex flex-1 items-center justify-center sm:items-stretch sm:justify-start">
        <div class="text-4xl font-bold">
          m.
        </div>
        <div class="hidden sm:ml-6 sm:block">
          <div class="flex space-x-4 link-container">
            <!-- Current: "bg-gray-900 text-white", Default: "text-gray-300 hover:bg-gray-700 hover:text-white" -->
            <a
              v-for="(link, index) in links"
              :key="index"
              href="#"
              @click.prevent="toggleActive(index)"
              :class="[
                'rounded-md px-3 py-2 text-md font-bold',
                active_index === index
                  ? 'bg-gray-900 text-white'
                  : 'text-gray-300 hover:bg-gray-700 hover:text-white'
              ]"
              :aria-current="active_index.value === index ? 'page' : null"
            >
              {{ link }}
            </a>
          </div>
        </div>
      </div>
      <div class="absolute inset-y-0 right-0 flex items-center pr-2 sm:static sm:inset-auto sm:ml-6 sm:pr-0">
        <!-- Profile dropdown -->
        <div class="relative ml-3">
          <div>
            <a href="https://www.linkedin.com/in/michael-joshua-sarmiento-8182992ab/" class="cursor-pointer" target="_blank">
              <img :src="linkedin_logo" class="size-10" alt="Logo" />
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Mobile menu, show/hide based on menu state. -->
  <div v-if="hamburger_state" class="sm:hidden" id="mobile-menu">
    <div class="space-y-1 px-2 pt-2 pb-3">
      <a
        v-for="(link, index) in links"
        :key="index"
        href="#"
        @click.prevent="toggleActive(index)"
        :class="[
          'block rounded-md px-3 py-2 text-base font-medium',
          active_index === index
            ? 'bg-gray-900 text-white'
            : 'text-gray-300 hover:bg-gray-700 hover:text-white'
        ]"
        :aria-current="active_index.value === index ? 'page' : null"
      >
        {{ link }}
      </a>
    </div>
  </div>
</nav>

<component :is="currentSection" class="p-6" />
  
</template>

<style scoped>

</style>

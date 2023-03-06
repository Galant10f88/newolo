<script setup>
import { containerMaxW } from "@/config.js";
import BaseLevel from "@/components/BaseLevel.vue";
import JustboilLogo from "@/components/JustboilLogo.vue";

const year = new Date().getFullYear();
</script>

<template>
  <footer class="py-2 px-6" :class="containerMaxW">
    <BaseLevel>
      <div class="relative text-cyan-400 text-center md:text-left">
        <b
          >&copy;{{ year }},
          <a href="https://cryptable.netlify.app/" target="_blank">GALANT WAS HERE</a>.</b
        >
        <slot />
      </div>
      <div class="md:py-2">
        
      </div>
    </BaseLevel>
  </footer>
</template>

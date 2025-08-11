<script lang="ts" setup>
import { Cog } from "lucide-vue-next";

const route = useRoute();
const runtimeConfig = useRuntimeConfig();
const appConfig = useAppConfig();

const showDebugPanel = defineModel<boolean>();
</script>

<template>
  <div class="border-b relative bg-[#007eb1]">
    
    <!-- <div class="bg-[#003647] h-11 secondary-nav"></div> -->

    <div class="container mx-auto px-4 pt-2 min-h-[67px]">
      <img src="/qg-coa-white.svg" alt="Queensland Government" class="h-[50px]" />
    </div>

    <nav
      class="main-nav container mx-auto px-4 pt-1 pb-3 hidden md:flex md:flex-row gap-3"
    >
      <NuxtLink
        v-for="{ label, url } in appConfig.menu.filter(
          (item) => item.active !== false
        )"
        :to="url"
        :class="`nav-btn hover:border-primary transition-all p-2 rounded-md text-[15px] font-sans font-[500] hover:text-primary hover:bg-white ${
          (url === '/' && route.path === '/') ||
          (url !== '/' && route.path.startsWith(url))
            ? 'text-primary border-primary bg-white p-2'
            : 'border-transparent text-white'
        }`"
        >{{ label }}</NuxtLink
      >

      <!-- debug -->
      <div v-if="runtimeConfig.public.prezDebug" class="!ml-auto">
        <div v-if="showDebugPanel">
          <span
            title="Toggle debug off"
            class="hover:cursor-pointer hover:text-gray-500 text-blue-400"
            @click="
              () => {
                showDebugPanel = !showDebugPanel;
              }
            "
          >
            <Cog class="w-4 h-4" />
          </span>
        </div>
        <span
          v-else
          title="Toggle debug on"
          class="hover:cursor-pointer hover:text-gray-500 text-gray-300"
          @click="
            () => {
              showDebugPanel = !showDebugPanel;
            }
          "
        >
          <Cog class="w-4 h-4" />
        </span>
      </div>
    </nav>
  </div>
</template>

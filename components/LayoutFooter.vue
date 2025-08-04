<script lang="ts" setup>
const runtimeConfig = useRuntimeConfig();
const globalConfig = useGlobalConfig();
const apiEndpoint = useGetPrezAPIEndpoint();
const altEndpoints = useGetPrezAPIAltEndpoints();
</script>

<template>
  <footer class="bg-tertiary text-tertiary-foreground pt-6 pb-10">
    <div class="container mx-auto text-center">
      <div class="text-sm">
        <div>
          Prez UI v{{ runtimeConfig.app.version }} -
          <a
            href="https://github.com/RDFLib/prez-ui"
            target="_blank"
            rel="noopener noreferrer"
            >GitHub</a
          >
        </div>
        <div v-if="globalConfig?.version">
          Prez API v{{ globalConfig?.version }} -
          <a
            href="https://github.com/RDFLib/prez"
            target="_blank"
            rel="noopener noreferrer"
            >GitHub</a
          >
        </div>
      </div>

      <!-- endpoints -->
      <div
        v-if="
          apiEndpoint != runtimeConfig.public.prezApiEndpoint &&
          !altEndpoints.find((e) => e.endpoint == apiEndpoint)
        "
      >
        <em
          ><small>custom override API endpoint {{ apiEndpoint }}</small></em
        >
      </div>
      <ul
        v-if="altEndpoints.length > 0"
        class="flex space-x-1 text-sm text-gray-400 justify-center [&>li:not(:last-child)]:after:content-['|'] [&>li:not(:last-child)]:after:mx-2"
      >
        <li
          class="hover:cursor-pointer"
          v-for="{ endpoint, name } of [
            { name: 'Default', endpoint: runtimeConfig.public.prezApiEndpoint },
            ...altEndpoints,
          ]"
        >
          <a
            :class="apiEndpoint == endpoint ? '!text-yellow-200' : ''"
            :href="`/?_api=${endpoint}`"
            >{{ name }}</a
          >
        </li>
      </ul>
    </div>
  </footer>

  <footer
    class="pt-1 bg-[#0C2E4C] text-white hover:decoration-white font-sans text-[11.2px]"
  >
    <div class="container mx-auto px-4 pt-7 pb-8">
      <ul class="flex justify-center gap-3 divide-x mb-6">
        <li>
          <a href="https://www.qld.gov.au/contact-us" class="footer-link"
            >Contact us</a
          >
        </li>
        <li class="hidden">
          <a href="https://www.qld.gov.au/help" class="footer-link">Help</a>
        </li>
        <li>
          <a
            href="https://www.qld.gov.au/legal/copyright"
            class="footer-link pl-3"
            >Copyright</a
          >
        </li>
        <li>
          <a
            href="https://www.qld.gov.au/legal/disclaimer"
            class="footer-link pl-3"
            >Disclaimer</a
          >
        </li>
        <li>
          <a
            href="https://www.qld.gov.au/legal/privacy"
            class="footer-link pl-3"
            >Privacy</a
          >
        </li>
        <li>
          <a
            href="https://www.qld.gov.au/about/rights-accountability/right-to-information"
            class="footer-link pl-3"
            >Right to information</a
          >
        </li>
        <li class="hidden">
          <a
            href="https://www.qld.gov.au/help/accessibility"
            class="footer-link"
            >Accessibility</a
          >
        </li>
        <li class="hidden">
          <a href="http://www.smartjobs.qld.gov.au/" class="footer-link"
            >Jobs in Queensland Government</a
          >
        </li>
        <li id="link-languages">
          <a
            href="https://www.qld.gov.au/help/languages"
            class="footer-link pl-3"
            >Other languages</a
          >
        </li>
      </ul>

      <p class="text-center text-[10.7px] font-[450] tracking-tight text-white mb-2">
        © The State of Queensland 1995-2025
      </p>
      <p
        class="text-center text-[10.7px] font-[450] tracking-tight text-white"
      >
        <a href="https://www.qld.gov.au" class="footer-link underline"
          >Queensland Government</a
        >
      </p>
    </div>
  </footer>
</template>

<template>
  <v-container class="home">
    <hello-world msg="Welcome to Your Vue.js + TypeScript App" />
    <teleport to="head">
      <meta
        name="keyword"
        content="template, typescript, vue2, vite, vite-template, composition-api, volar"
      />
      <meta name="description" content="Vite Vue2 TypeScript Demo" />
      <component :is="'script'" type="application/ld+json">
        {{ jsonLd }}
      </component>
    </teleport>
  </v-container>
</template>

<script lang="ts">
import { defineComponent, watch, type SetupContext } from 'vue';

// import { useStore } from '@logue/vue2-helpers/vuex';
import { useRoute } from 'vue-router/composables';

import logo from '@/assets/vuetify.svg';
import HelloWorld from '@/components/HelloWorld.vue';

/** Home Component */
export default defineComponent({
  /** Components */
  components: {
    HelloWorld,
  },
  /**
   * Setup
   *
   * @param _props - Props
   * @param _context - Context
   */
  setup(_props, _context: SetupContext) {
    /** Route */
    const route = useRoute();
    /** Vuex */
    // const store = useStore();

    /** JSON LD sample */
    const jsonLd = JSON.stringify(
      {
        '@schema': 'https://json.schemastore.org/jsonld.json',
        '@context': 'http://schema.org',
        '@type': 'WebSite',
        name: 'Vite Vue2 TypeScript Startar',
        url: 'https://github.com/logue/vite-vue2-vuetify-ts-starter',
        description: 'Vite Vue2 TypeScript Demo Page',
        logo,
      },
      null,
      2
    );

    /* *
     * Computed
     * /
    const computedValue: Ref<string> = computed({
      get: () => store.getters.computedValue,
      set: v => store.dispatch('setComputedValue', v)
    }
     */

    // Watch
    watch(
      () => route?.name,
      name => console.log('route is changed:', name)
    );

    return {
      jsonLd,
    };
  },
});
</script>

<script lang="ts" setup>
  import { ref } from 'vue';
  import NavigationItems from '@/components/Navigation/NavigationItems.vue';
  import { Section } from '@/data';

  const selectedSection = ref<Section>();

  const switchSection = (section: Section) => {
    selectedSection.value = section;
  };
</script>

<template>
  <div class="pr-8 pb-6 border-b border-gray-400">
      <SectionsToggle @switch="switchSection" />
    </div>
  <div>
    <NavigationItems :key="selectedSection.id" class="pt-6 pr-8" :selected-section="selectedSection" v-if="!!selectedSection?.path" />
  </div>
</template>

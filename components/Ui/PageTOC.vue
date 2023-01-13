<script setup lang="ts">
  import { useTOC } from '@/composables';
  import { Link, PageTOC } from '@/components/Ui';
  import TocItem from '@/components/Toc/TocItem.vue';

  const { toc, displayTOC } = useTOC();
  const selectedSection = ref(toc.value.links[0].id);

  const switchSection = (section: string) => {
    selectedSection.value = section;
  };
</script>

<template>
  <div class="w-[200px] flex-shrink-0" v-if="displayTOC">
    <TocItem
      :key="item.id"
      v-for="item in toc.links"
      :selectedItem="item"
      @switchSection="switchSection"
      :selectedSection="selectedSection"
    />
  </div>
</template>

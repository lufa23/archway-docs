<script setup lang="ts">
  import { Link } from '@/components/Ui';
  import { PropType, ref } from 'vue';
  import { PageTOC } from '@/domain';
  import TocItem from '@/components/Toc/TocItem.vue';

  const emit = defineEmits(['switchSection']);

  defineProps({
    selectedItem: { type: Object as PropType<PageTOC>, required: true },
    selectedSection: { type: Object as PropType<string>, required: true },
  });
</script>

<template>
  <div
    :key="selectedItem.id"
    :class="{
      'border-orange': selectedSection === selectedItem.id && !selectedItem.children,
      'border-l': selectedSection === selectedItem.id && !selectedItem.children,
      'pl-4': selectedItem.children,
    }"
    class="mt-4"
  >
    <Link @click="emit('switchSection', selectedItem.id)" :href="'#' + selectedItem.id"
      ><p :class="{ 'text-orange': selectedSection === selectedItem.id, 'pl-4': !selectedItem.children }">
        {{ selectedItem.text }}
      </p></Link
    >
    <TocItem
      :key="selectedItem.id"
      v-for="item in selectedItem.children"
      :selectedItem="item"
      @switchSection="item => emit('switchSection', item)"
      :selectedSection="selectedSection"
    />
  </div>
</template>

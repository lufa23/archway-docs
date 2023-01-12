<script lang="ts" setup>
  import { PropType } from 'vue';
  import NavigationItem from '@/components/Navigation/NavigationItem.vue';
  import { Section, useNavigation } from '@/data';

  const props = defineProps({
    selectedSection: { type: Object as PropType<Section>, required: true },
  });
  const route = useRoute();

  const { navigation } = await useNavigation(props.selectedSection);
  const selectedSection = ref(route.path);

  const switchSection = (section: Section) => {
    selectedSection.value = section;
  };
</script>

<template>
  <div class="space-y-4">
    <NavigationItem :item="item" v-for="item in navigation" @switchSection="switchSection" :selectedSection="selectedSection" />
  </div>
</template>

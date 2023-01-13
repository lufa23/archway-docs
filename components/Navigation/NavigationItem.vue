<script lang="ts" setup>
  import { PropType, ref } from 'vue';
  import { Link, ChevronRightIcon, ChevronDownIcon } from '@/components/Ui';
  import NavigationItem from '@/components/Navigation/NavigationItem.vue';
  import { NavigationItem as NavigationItemType } from '@/domain';
  import { Section } from '@/data';

  const props = defineProps({
    item: { type: Object as PropType<NavigationItemType>, required: true },
    selectedSection: { type: Object as PropType<string>, required: true },
  });

  const route = useRoute();

  const emit = defineEmits(['switchSection']);

  let doesSelectedItemChildExist = false;
  const isChildExist = (dataItem = []) => {
    dataItem.forEach(data => {
      if (data.children.length) {
        isChildExist(data.children);
      }
      if (data.path === props.selectedSection) {
        doesSelectedItemChildExist = true;
      }
    });
  };

  isChildExist(props.item.children);

  const shouldOpen = ref(props.selectedSection === props.item.path || doesSelectedItemChildExist);
</script>

<template>
  <div>
    <div v-if="item.children.length" class="flex items-center cursor-pointer" @click="shouldOpen = !shouldOpen">
      <p class="mr-2" v-if="!shouldOpen"><ChevronRightIcon class="w-4 h-4" /></p>
      <p class="mr-2" v-else><ChevronDownIcon class="w-4 h-4" /></p>
      <p>{{ item.title }}</p>
    </div>
    <div v-else @click="emit('switchSection', item.path)">
      <Link :href="item.path"
        ><p :class="{ 'text-orange': selectedSection === item.path }">{{ item.title }}</p></Link
      >
    </div>
    <div class="pl-3 mt-2">
      <div class="pl-6 pt-2 border-l border-gray-400" v-if="item.children.length" v-show="shouldOpen">
        <NavigationItem
          :item="child"
          v-for="child in item.children"
          @switchSection="path => emit('switchSection', path)"
          :selectedSection="selectedSection"
        />
      </div>
    </div>
  </div>
</template>

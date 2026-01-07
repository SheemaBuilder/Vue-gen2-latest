<!-- <script setup lang="ts">
//import { VContainer } from 'vuetify/components';
import { computed } from 'vue';

//import type { IBreadcrumbs } from '../components/cms/HBreadcrumb/HBreadcrumb.d';

//import Breadcrumbs from '~vue/components/util/Breadcrumbs/Breadcrumbs.ts.vue';

defineOptions({
  inheritAttrs: false,
});

interface RegistrationBreadcrumbs {
  title?: string;
  slug?: string;
}

interface Props {
  title?: string;
  subtitle?: string;
  showBreadcrumbs?: boolean;
  breadcrumbs?: RegistrationBreadcrumbs[];
}

const props = withDefaults(defineProps<Props>(), {
  title: undefined,
  subtitle: undefined,
  showBreadcrumbs: false,
  breadcrumbs: () => ([]),
});

const breadcrumbItems = computed((): IBreadcrumbs[] => {
  if (!props.breadcrumbs) return [];

  const items: IBreadcrumbs[] = [{
    text: 'Home',
    to: '/',
  }];

  props.breadcrumbs.forEach(({ title, slug }: RegistrationBreadcrumbs, index: number) => {
    if (!slug?.trim()) return;

    items.push({
      text: title?.trim() ?? '',
      to: slug?.trim() ?? '',
      disabled: index === props.breadcrumbs.length - 1,
    });
  });

  return items;
});
</script>

<template>
  <VContainer id="page-header">
    <Breadcrumbs
      v-if="showBreadcrumbs && breadcrumbs.length"
      class="dds-mb-4"
      :items="breadcrumbItems"
      data-za="breadcrumbs"
    />
    <hgroup>
      <h1 class="text-h1">
        {{ title }}
      </h1>
      <h2
        v-if="subtitle"
        class="dds-sub dds-mt-4 dds-mb-0 subtitle"
      >
        {{ subtitle }}
      </h2>
    </hgroup>
  </VContainer>
</template>
<style scoped lang="scss">
.subtitle {
  font-size: $size-3;
}
</style> -->

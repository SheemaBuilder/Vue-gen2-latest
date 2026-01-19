<script setup lang="ts">
  import {
    Content,
    fetchOneEntry,
    isPreviewing,
    type BuilderContent,
    getBuilderSearchParams,
  } from '@builder.io/sdk-vue';
  import { onMounted, ref } from 'vue';
  
  import HelloWorldComponent from './components/HelloWorld.vue';
  //import PageHeader from './components/PageHeader.vue';
  
  // Register your Builder components
  const REGISTERED_COMPONENTS = [
    {
      component: HelloWorldComponent,
      name: 'Hello World',
      canHaveChildren: true,
      shouldReceiveBuilderProps: {
        builderContext: true,
      },
      inputs: [
        {
          name: 'text',
          type: 'string',
          defaultValue: '',
        },
      ],
    },
    //{
    //   component: PageHeader,
    //   name: 'Page Header',
    //   canHaveChildren: false,
    //   inputs: [
    //     {
    //       name: 'title',
    //       type: 'string',
    //       helperText: 'The H1 text',
    //     },
    //     {
    //       name: 'subtitle',
    //       type: 'string',
    //       helperText: 'The H2 text',
    //     },
    //     {
    //       name: 'showBreadcrumbs',
    //       type: 'boolean',
    //       defaultValue: false,
    //       helperText: 'Enable to show breadcrumbs',
    //     },
    //     {
    //       name: 'breadcrumbs',
    //       type: 'list',
    //       helperText: 'Enter each crumb, no need to create home it\'ll be auto generated',
    //       subFields: [
    //         {
    //           name: 'title',
    //           type: 'string',
    //           defaultValue: '',
    //           helperText: 'Enter the user-facing title of the link (e.g. Your Path)',
    //         },
    //         {
    //           name: 'slug',
    //           type: 'string',
    //           defaultValue: '',
    //           helperText: 'Enter the url path e.g. /your-url-path/',
    //           regex: urlFieldValidationHandler,
    //         },
    //       ],
    //     },
    // }
  ];
  
  // TODO: enter your public API key
  const BUILDER_PUBLIC_API_KEY = ''; // ggignore
  const content = ref<BuilderContent | null>(null);
  const canShowContent = ref(false);
  const model = 'page';
  
  onMounted(async () => {
    content.value = await fetchOneEntry({
      model,
      apiKey: BUILDER_PUBLIC_API_KEY,
      options: getBuilderSearchParams(new URL(location.href).searchParams),
      userAttributes: {
        urlPath: window.location.pathname,
      },
    });
    canShowContent.value = content.value ? true : isPreviewing();
  });
  </script>
  
  <template>
    <header>
      <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />
    </header>
    <div>
      <div>Hello world from your Vue 3 project. Below is Builder Content:</div>
      <div v-if="canShowContent">
        <div>
          page title:
          {{ (content && content.data && content.data.title) || 'Unpublished' }}
        </div>
        <Content
          :model="model"
          :content="content"
          :api-key="BUILDER_PUBLIC_API_KEY"
          :customComponents="REGISTERED_COMPONENTS"
        />
      </div>
      <div v-else>Content not Found</div>
    </div>
  </template>
  
  <style>
  #app {
    margin: 0 auto;
    padding: 2rem;
  
    font-weight: normal;
  }
  </style>

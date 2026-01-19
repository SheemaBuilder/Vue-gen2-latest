<template>
  <div class="hello-world">
    <div class="text">Hello {{ builderContext.content.data.title }}!</div>
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: {
    text: {
      type: String,
      default: '',
    },
    builderContext: {
      type: Object,
      default: () => ({}),
    },
  },
};
</script>

<style scoped>
.hello-world {
  display: flex;
  flex-direction: column;
}
.text {
  padding: 50px;
}
</style>
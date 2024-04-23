<template>
  <div>
    <img :src="src" :alt="alt" class="custom-image" />
  </div>
</template>

<script>
export default {
  name: 'CustomImage',
  props: {
    src: String,
    alt: String,
  },
};
</script>

<style scoped>
.custom-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  cursor: pointer;
}
</style>

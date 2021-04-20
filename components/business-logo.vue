<template>
  <div class="elevation-3 business-logo">
    <img :alt="alt || 'logo'" :src="src || require('@/static/no-image.png')" />
  </div>
</template>

<script>
export default {
  props: {
    src: {
      type: String,
      default: '',
    },
    alt: {
      type: String,
      default: '',
    },
  },
}
</script>

<style lang="scss" scoped>
@import '@/assets/_vuetifycomponents';
@import '@/assets/_variables';

.business-logo {
  position: absolute;
  left: -20px;
  top: 35px;
  width: 100px;
  height: 100px;
  border-radius: 25%;
  overflow: hidden;
  box-sizing: border-box;
  background-color: $colorPrimaryWhite;
}

.business-logo img {
  object-fit: contain;
  height: 100%;
  width: 100%;
}
</style>

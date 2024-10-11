<template>
  <div class="banner-container">
    <img :src="bannerImage" alt="Banner" class="banner-image" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      bannerImage: require('@/assets/banner.png')
    };
  }
};
</script>

<style scoped>
.banner-container {
  overflow: hidden;
}

.banner-image {
  width: 100%;
  height: auto;
  display: block;
}
</style>

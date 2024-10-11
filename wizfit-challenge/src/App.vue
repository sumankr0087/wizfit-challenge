<template>
  <div id="app">
    <HeaderBanner />
    <HeroSection />
    <SchoolList />
  </div>
</template>

<script>
import HeaderBanner from './components/HeaderBanner.vue'
import HeroSection from './components/HeroSection.vue'
import SchoolList from './components/SchoolList.vue';

export default {
  components: {
    HeaderBanner,
    HeroSection,
    SchoolList
  }
}
</script>

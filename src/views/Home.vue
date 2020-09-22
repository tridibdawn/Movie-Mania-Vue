<template>
  <div class="home">
    <home-carousel></home-carousel>
  </div>
</template>

<script>
import HomeCarousel from '../components/home/HomeCarousel.vue';
export default {
  name: 'Home',
  components: {
    "home-carousel": HomeCarousel
  }
}
</script>

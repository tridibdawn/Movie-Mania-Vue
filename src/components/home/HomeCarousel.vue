<template>
  <div>
    <b-carousel
      id="carousel-1"
      v-model="slide"
      :interval="4000"
      controls
      indicators
      background="#ababab"
      img-width="1024"
      img-height="320"
      style="text-shadow: 1px 1px 2px #333;"
      @sliding-start="onSlideStart"
      @sliding-end="onSlideEnd"
    >
      <!-- Text slides with image -->
      <b-carousel-slide
        caption="Star Wars Andromeda"
        text="Coming Soon"
        img-src="https://c4.wallpaperflare.com/wallpaper/736/411/582/star-wars-star-wars-the-rise-of-skywalker-movie-poster-poster-movie-characters-hd-wallpaper-preview.jpg"
      ></b-carousel-slide>
      <!-- Slides with custom text -->
      <b-carousel-slide img-src="https://c4.wallpaperflare.com/wallpaper/502/419/818/the-dark-knight-batman-movies-wallpaper-preview.jpg">
        <h1>Batman - Arkham Knight</h1>
      </b-carousel-slide>
      <!-- Slides with image only -->
      <b-carousel-slide img-src="https://c4.wallpaperflare.com/wallpaper/123/991/646/avatar-blue-skin-james-cameron-s-movie-avatar-movie-poster-wallpaper-preview.jpg"></b-carousel-slide>
      <b-carousel-slide>
        <template v-slot:img>
          <img
            class="d-block img-fluid w-100"
            width="1024"
            height="320"
            src="https://c4.wallpaperflare.com/wallpaper/156/167/750/movies-thor-chris-hemsworth-black-background-wallpaper-preview.jpg"
            alt="image slot"
          >
        </template>
      </b-carousel-slide>
    </b-carousel>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        slide: 0,
        sliding: null
      }
    },
    methods: {
      onSlideStart() {
        this.sliding = true
      },
      onSlideEnd() {
        this.sliding = false
      }
    }
  }
</script>
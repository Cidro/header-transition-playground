<template>
  <div id="app">
    <div class="header">
      <transition name="carousel">
        <div
            v-if="activeImage === index"
            v-for="(image, index) in images"
            :key="`image-${index}`"
            class="carousel--image"
            :style="{backgroundImage: `url(${image})`}">
        </div>
      </transition>
    </div>
    <div class="controls">
      <button @click.prevent="handleClickToggleImage">Toggle Image</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      images: [
        'https://loremflickr.com/cache/resized/1445_25203757810_5398265784_h_1280_400_nofilter.jpg',
        'https://loremflickr.com/cache/resized/7476_16324198586_f695542401_h_1280_160_nofilter.jpg'
      ],
      activeImage: 0
    }
  },
  methods: {
    handleClickToggleImage() {
      this.activeImage = this.activeImage === 0 ? 1 : 0
    }
  }
}
</script>

<style lang="scss">
@import "styles/reset.css";
#app {
  font-family: Helvetica, Arial, SansSerif, serif;
  font-size: 2rem;
  width: 100vw;
  min-height: 100vh;

  .header {
    width: 100vw;
    min-height: 25vh;
    position: relative;
    background-color: #eee;
    overflow: hidden;
    perspective: 1000px;
    transform-style: preserve-3d;
  }

  .controls {
    margin-top: 5vh;
    text-align: center;
  }
}

.carousel {
  &--image {
    height: 25vh;
    width: 100%;
  }
  &-enter-active {
    opacity: 0;
    z-index: 9999;
    animation: carousel-enter 0.5s linear 0.25s;
  }
  &-leave-active {
    position: absolute;
    top: 0;
    left: 0;
    opacity: 1;
    z-index: 9998;
    animation: carousel-leave 0.5s linear;
  }
}

@keyframes carousel-enter {
  0% {
    opacity: 0;
    transform: translate3d(400px, 0, -200px);
  }

  33% {
    transform: translate3d(266px, 0, -200px);
  }

  66% {
    transform: translate3d(133px, 0, -200px);
  }

  100% {
    opacity: 1;
    transform: translate3d(0, 0, 0);
  }
}

@keyframes carousel-leave {
  0% {
    opacity: 1;
    transform: translate3d(0, 0, 0);
  }

  33% {
    transform: translate3d(-133px, 0, -200px);
  }

  66% {
    transform: translate3d(-266px, 0, -200px);
  }

  100% {
    opacity: 0;
    transform: translate3d(-400px, 0, -200px);
  }
}
</style>

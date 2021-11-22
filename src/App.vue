<template>
  <section class="main" ref="main">
    <video class="video" ref="video" src="https://www.dr.dk/tjenester/netdoks/sugardaters_dagbog/video/start_d_slow_v03.mp4"/>
  </section>
  <section class="section">
    <div>
      On Scroll play video demo
    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'App',
  data() {
    return {
      scrollTop: 0,
    }
  },
  methods: {
    onScrollHandler() {
      const main = this.$refs['main'] as HTMLElement;
      var video = this.$refs['video'] as HTMLVideoElement;

	    const videoLength = video.duration;
	    const scrollPosition = window.scrollY;

	    video.currentTime = (scrollPosition / main.clientHeight) * videoLength;
    },
  },
  mounted() {
    const main = this.$refs['main'] as HTMLElement;
    window.addEventListener('scroll', this.onScrollHandler);
  },
  unmounted() {
    const main = this.$refs['main'] as HTMLElement;
    window.removeEventListener('scroll', this.onScrollHandler);
  }
});
</script>

<style>
body {
  margin: 0;
}

.main {
  width: 100%;
  height: 4000px;
  position: relative;
}

.section {
  height: 100vh;
  background-color: #020102;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  padding: 40px;
  text-align: center;
}

.video {
  width: 100%;
  object-fit: cover;
  height: 100vh;
  position: sticky;
  left: 0;
  top: 0;
  z-index: -1;
}
</style>

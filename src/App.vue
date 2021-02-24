<template>
  <div id="app">
    <div class="container">
      <div class="container_media">
        <video
          class="container_media-video"
          src="./assets/galaxy-video.mp4"
          autoplay
          muted
          loop
        ></video>
      </div>
      <Game></Game>
    </div>
  </div>
</template>

<script>
import Game from './components/Game/Game'

export default {
  name: 'App',
  components:{
    Game,
  }
}
</script>

<style >
@import './App.css';

</style>

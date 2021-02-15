<template>
  <div id="wrapper">
    <img id="logo" src="~@/assets/logo.png" alt="electron-vue">
    <main>
      <div class="software-info">
        <h1 class="title">
          Welcome to simple video player.
        </h1>
        <div  class="slogan">
          Just select file, then play it.
        </div>
      </div>
      <div class="video-test">
        <video
        id="video-player"
        class="video-js"
        controls
        preload="auto"
        data-setup="{}"
        ref="player"
        >
      </video>
    </div>
    <div class="button-wrapper">
      <button class="btn" v-on:click="selectFile">Open File</button>
    </div>
  </main>
</div>
</template>

<script>
import videojs from 'video.js';
import 'video.js/dist/video-js.css';
export default {
  name: 'Home',
  methods: {
    async selectFile(){
      const dialog = this.$electron.remote.dialog;
      const files = dialog.showOpenDialog({
        properties: ['openFile'],
        filters: {
          "name": "video",
          "extensions": ['mp4'],
        },
      });
      const file = files[0];
      if(file){
        const video = `file:///${file}`;
        const videoPlayerEle = this.$refs.player;
        const videoPlayer = videojs(videoPlayerEle);
        videoPlayer.src(video);
      }
    },
  },
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body { font-family: 'Source Sans Pro', sans-serif; }

#wrapper {
  background:
  radial-gradient(
  ellipse at top left,
  rgba(255, 255, 255, 1) 40%,
  rgba(229, 229, 229, .9) 100%
  );
  height: 100vh;
  padding: 60px 80px;
  width: 100vw;
}

#logo {
  height: auto;
  margin-bottom: 20px;
  width: 25%;
  margin-left: auto;
  margin-right: auto;
  display: block;
}

.software-info{
  text-align: center;
  .slogan{
    font-size: 1.1em;
    margin-top: 20px;
  }
}
.button-wrapper{
  text-align: center;
  margin-top:  30px;
}
</style>

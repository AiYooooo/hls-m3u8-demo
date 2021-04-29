<template>
  <div id="app">
    <video ref="videoElement" id="videoElement" autoplay muted></video>
  </div>
</template>

<script>
let Hls = require('hls.js');
export default {
  name: 'App',
  components: {
    
  },
  data: function() {
    return {
      hls: ''
    }
  },
  mounted() {
    this.loadFlv();
  },
  methods: {
    loadFlv(){
      if (Hls.isSupported()) {
        this.hls = new Hls();
        this.hls.loadSource('');
        this.hls.attachMedia(this.$refs.videoElement);
        this.hls.on(Hls.Events.MANIFEST_PARSED, () => {
          console.log('加载成功');
          this.$refs.video.play();
        });
        this.hls.on(Hls.Events.ERROR, (event, data) => {
          console.log(event, data);
          // 监听出错事件
          console.log('加载失败');
        });
      }
    },
    videoPause() {
      if (this.hls) {
        this.$refs.videoElement.pause();
        this.hls.destroy();
        this.hls = null;
      }
    },
  },
  beforeDestroy() {
    this.videoPause();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  box-sizing: border-box;
}

video {
  width: 100%;
  height: 100%;
}
</style>

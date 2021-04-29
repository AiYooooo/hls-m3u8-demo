<template>
  <div id="app">
    <video ref="videoElement" id="videoElement" autoplay muted></video>
  </div>
</template>

<script>
import flvjs from 'flv.js'
export default {
  name: 'App',
  components: {
    
  },
  mounted() {
    this.loadFlv();
  },
  methods: {
    loadFlv(){
      let video =this.$refs.videoElement//定义播放路径
      if(flvjs.isSupported()){
        this.player = flvjs.createPlayer({
          type: 'flv',
          hasAudio: false,
          url: 'http://192.168.105.149:30210/live/live_315_1.flv?token=eyJrZXkiOjI4NCwic2lnbiI6InhCazdwcmFiQmViVllpazlzY1M2RDlBOFJVR1lyaEltald6RXJIdHpGMzdzMlZZb0F0TnlXRWNyWXc1czlDOUNQQVNXeG5mQ0VLOTBrSzlsYjNhUUdvYWVKLWZENEdwWDhoeGVuWkl2Q1RHSDgxYjBuU0dwMDFNRFRyNkJOd3dtUTZFTFpKWEpkcU9HbTE2aGlFQ1JCcVFiV3BZRWl4ZXIyNDZ6Uk95bG9KayJ9'
        });
      }else{
        return;
      }
      this.player.attachMediaElement(video)
      this.player.load()
      this.player.play()
    },
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

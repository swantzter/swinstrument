<template>
  <div class="container">
    <div class="grid">
      <TonePanel note="C5" @play="play" @click="particles" />
      <TonePanel note="G5" @play="play" @click="particles" />
      <TonePanel note="A5" @play="play" @click="particles" />

      <TonePanel note="B4" @play="play" @click="particles" />
      <TonePanel note="E5" @play="play" @click="particles" />
      <TonePanel note="B5" @play="play" @click="particles" />

      <TonePanel note="D5" @play="play" @click="particles" />
      <TonePanel note="F5" @play="play" @click="particles" />
      <TonePanel note="C6" @play="play" @click="particles" />
    </div>
    <Particles :new-touch="newTouch" @rendered="newTouchHandled" />
  </div>
  <Intro />
</template>

<script>
import TonePanel from './components/TonePanel.vue'
import Particles from './components/Particles.vue'
import Intro from './components/Intro.vue'
import { Synth, start } from 'tone'

export default {
  name: 'App',
  components: {
    TonePanel,
    Particles,
    Intro
  },
  data: () => ({
    started: false,
    newTouch: null
  }),
  computed: {
    synth: () => (new Synth().toDestination('master'))
  },
  methods: {
    async play (tone) {
      if (!this.started) {
        await start()
        this.started = true
      }
      this.synth.triggerAttackRelease(tone, '8n')
    },
    newTouchHandled () {
      this.newTouch = null
    },
    particles ({ x, y }) {
      this.newTouch = { x, y }
    }
  }
}
</script>

<style scoped>
  .container {
    height: 50vh;
    border-bottom-left-radius: 50% 3vh;
    border-bottom-right-radius: 50% 3vh;
    overflow: hidden;
    position: relative;
    z-index: 0;
  }

  .container {
    background: #5f9242;
    background: linear-gradient(135deg, rgba(155,176,83,1) 0%, rgba(39,118,50,1) 100%);
  }

  .grid {
    display: grid;
    grid-template-rows: 1fr 1fr 1fr;
    grid-template-columns: 1fr 1fr 1fr;
    height: 100%;
    z-index: 1;
  }
</style>

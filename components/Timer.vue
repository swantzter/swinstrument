<template>
  <div class="wrapper">
    <div class="bar" :class="{ started: state === 'started' }" @click="toggle">
      <span v-if="state === 'stopped'">Start</span>
      <template v-else-if="state === 'started'">
        <div class="progress" :style="{ width }"></div>
        <span>{{ clockTime }}</span>
      </template>
      <span v-else-if="state === 'ended'">Clear</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Timer',
  data: () => ({
    state: 'stopped',
    time: null,
    precise: null,
    interval: null
  }),
  computed: {
    clockTime () {
      const minutes = Math.floor(this.time / 60).toString().padStart(2, '0')
      const seconds = (this.time % 60).toString().padStart(2, '0')

      return `${minutes}:${seconds}`
    },
    width () {
      return `${Math.round(this.precise / 180 * 10000) / 100}%`
    }
  },
  methods: {
    toggle () {
      switch (this.state) {
        case 'stopped':
          return this.start()
        case 'started':
          return this.stop()
        case 'ended':
          return this.reset()
      }
    },
    start () {
      this.state = 'started'
      this.$emit('started')
      const self = this
      const start = (Date.now() / 1000)

      this.interval = setInterval(() => {
        const now = (Date.now() / 1000)
        const elapsed = now - start
        self.time = Math.round(180 - elapsed)
        self.precise = 180 - elapsed

        if (self.time <= 0) self.stop()
      }, 150)
    },
    stop () {
      this.state = 'ended'
      this.$emit('ended')
      clearInterval(this.interval)
      this.interval = null
    },
    reset () {
      this.state = 'stopped'
      this.$emit('reset')
      this.time = null
    }
  }
}
</script>

<style scoped>
  .wrapper {
    display: flex;
    justify-content: center;
    margin-right: 2rem;
    margin-left: 2rem;
  }

  .bar {
    display: inline-block;
    position: relative;
    background-color: transparent;
    border: 1px solid;
    border-radius: 4px;
    padding: .3rem;
    transition: .3s background-color, 1s width;
    text-align: center;
    width: 5rem;
  }

  .bar:not(.started):hover {
    background-color: rgba(24, 25, 27, .3);
  }

  @media (prefers-color-scheme: dark) {
    .bar:not(.started):hover {
      background-color: rgba(255, 255, 255, .3);
    }
  }

  .progress {
    height: 100%;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    background: #5f9242;
    background: linear-gradient(135deg, rgba(155,176,83,1) 0%, rgba(39,118,50,1) 100%);
    z-index: -1;
    transition: .1s width;
    width : 100%;
  }

  .started {
    width: 100%;
  }
</style>

<template>
  <canvas ref="canvas"></canvas>
</template>

<script>
export default {
  name: 'Particles',
  props: {
    newTouch: Object
  },
  data: () => ({
    ctx: null,
    particles: [],
    width: window.innerWidth,
    height: window.innerHeight / 2
  }),
  mounted () {
    const c = this.$refs.canvas
    const ctx = c.getContext('2d')
    this.ctx = ctx

    c.width = this.width
    c.height = this.height

    window.requestAnimationFrame(this.renderer)
  },
  watch: {
    async newTouch (newTouch) {
      if (!newTouch) return
      this.$emit('rendered', true)

      const { x, y } = newTouch
      const nParts = this.randI(3, 10)

      for (let i = 0; i <= nParts; i++) {
        if (this.particles.length > 50) this.particles.shift()
        this.particles.push({
          x,
          y,

          r: this.randF(1, 3),

          vx: this.randF(0.3, 2) * (Math.random() > 0.5 ? 1 : -1),
          vy: this.randF(0.3, 2) * (Math.random() > 0.5 ? 1 : -1),
          a: -this.randF(0, 1)
        })
      }
    }
  },
  methods: {
    randF (min, max) {
      return Math.random() * (max - min + 1)
    },
    randI (min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min
    },
    renderer () {
      const c = this.ctx

      c.clearRect(0, 0, this.width, this.height)
      c.fillStyle = 'rgba(255, 255, 255, 0.7)'
      c.filter = 'blur(2px)'
      c.save()

      for (let i = 0; i < this.particles.length; i++) {
        const p = this.particles[i]

        c.beginPath()
        c.arc(p.x, p.y, p.r, 0, Math.PI * 2, false)
        c.fill()

        p.x += p.vx
        p.y += p.vy

        // p.vx -= p.a
        // p.vy -= p.a

        if (
          p.x < 0 ||
          p.y < 0 ||
          p.x > this.width ||
          p.y > this.height
        ) {
          this.particles.splice(i, 1)
        }
      }

      window.requestAnimationFrame(this.renderer)
    }
  }
}
</script>


<style scoped>
  canvas {
    position: absolute;
    top: 0;
    left: 0;
    z-index: -1;
  }
</style>

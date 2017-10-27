<script>
import Vue from 'vue'
import { stagger, animation, bounceEaseOut } from './lib'

export default {
  render (h) {
    return <svg width="100vw" height="100vh" onclick={ this.move }>
      { this.circles.map(c => <circle fill="none" stroke-width="8" r={c.r} cx={c.cx} cy={c.cy} /> ) }
    </svg>
  },
  data () {
    return {
      circles: Array(25).fill('').map((e, i) => ({ r: 1 + (i * 5), cx: 100, cy: 150 }))
    }
  },
  methods: {
    move (e) {
      stagger(this.circles.map((circle, i) => {
        return animation(this.circles, i, { cx: e.x, cy: e.y }, {
          duration: 750,
          easing: bounceEaseOut
        })
      }), 50)()
    }
  }
}
</script>

<style lang="css">
body {
 background: #35495e;
}
.control {
 position: fixed;
 top: 0;
 left: 0
}
circle {
 stroke: rgba(65, 184, 131, 0.8);
 mix-blend-mode: screen;
}
</style>

<template lang="pug">
  <div class="home">
    HelloWorld(msg="Welcome to Your Vue.js App")
    div.background(ref='background' @mousedown='changeMapPos')
    h5(@click.prevent='addLocalStorage') 88888888
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import ProjectCard from '@/components/ProjectCard.vue'

export default {
  name: 'home',
  components: {
    HelloWorld,
    ProjectCard,
  },
  data() {
    return {
      isMapEvent: false,
      point: { x: 0, y: 0 },
    }
  },
  mounted() {
    this.initBackground()
    window.addEventListener('mouseup', this.mouseup)

    if (localStorage.getItem('test')) {
      console.log(7887)
    }
  },
  methods: {
    addLocalStorage() {
      localStorage.setItem('test', 1)
    },
    mouseup(e) {
      if (this.isMapEvent) {
        this.isMapEvent = false
      } else {
        // console.log('not isMapEvent')
      }
    },
    initBackground() {
      this.$refs.background.style.top = this.point.y + 'px'
      this.$refs.background.style.left = this.point.x + 'px'
    },
    changeMapPos(e) {
      this.isMapEvent = true
      this.point = { x: e.clientX, y: e.clientY }

      console.log(e)

      // this.$refs.background.addEventListener('mousemove', this.moveMap(event))
      this.$refs.background.addEventListener('mousemove', (event) => {
        if (this.isMapEvent) {
          console.log({
            clientY: event.clientY,
            clientX: event.clientX,
            offsetY: e.offsetY,
            offsetX: e.offsetX,
          })
          this.$refs.background.style.top = event.clientY - e.offsetY + 'px'
          this.$refs.background.style.left = event.clientX - e.offsetX + 'px'
        }
      })
    },
  },
}
</script>

<style scoped lang="scss">
.background {
  width: 500px;
  height: 500px;
  background: green;
  position: absolute;
  top: 0;
  left: 0;
}
</style>

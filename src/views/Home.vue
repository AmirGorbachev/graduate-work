<template lang="pug">
  div
    div.main-area(ref='main')
      HelloWorld(msg="Welcome to Your Vue.js App")
      div.background(ref='background' @mousedown='changeMapPos')
      h5(@click.prevent='addLocalStorage') 88888888
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
      // padding: 50,
      // isMovingRight: false,
      // isMovingLeft: false,
      // isMovingTop: false,
      // isMovingBottom: false,
    }
  },
  mounted() {
    this.initBackground()

    // const speed = 20

    // setInterval(() => {
    //   if (this.isMovingRight) {
    //     console.log(456)
    //     this.$refs.background.style.transform = `translate(${(this.point.x +=
    //       speed)}px, ${this.point.y}px)`
    //   }
    //   if (
    //     this.isMovingLeft &&
    //     this.$refs.background.getBoundingClientRect().left >
    //       this.$refs.main.getBoundingClientRect().left
    //   ) {
    //     this.$refs.background.style.transform = `translate(${(this.point.x -=
    //       speed)}px, ${this.point.y}px)`
    //   }
    //   if (this.isMovingTop) {
    //     this.$refs.background.style.transform = `translate(${
    //       this.point.x
    //     }px, ${(this.point.y += speed)}px)`
    //   }
    //   if (this.isMovingBottom) {
    //     this.$refs.background.style.transform = `translate(${
    //       this.point.x
    //     }px, ${(this.point.y -= speed)}px)`
    //   }

    //   console.log(this.$refs.background.getBoundingClientRect().left)
    //   console.log(this.$refs.main.getBoundingClientRect().left)
    // }, 100)

    this.$refs.main.addEventListener('mousemove', (event) => {
      if (event.clientX < this.padding) {
        this.isMovingRight = true
      } else if (
        event.clientX >
        this.$refs.main.getBoundingClientRect().width - this.padding
      ) {
        this.isMovingLeft = true
      } else {
        this.isMovingRight = false
        this.isMovingLeft = false
      }

      if (event.clientY < this.padding) {
        this.isMovingTop = true
      } else if (
        event.clientY >
        this.$refs.main.getBoundingClientRect().height - this.padding
      ) {
        this.isMovingBottom = true
      } else {
        this.isMovingTop = false
        this.isMovingBottom = false
      }
    })

    if (localStorage.getItem('test')) {
      console.log(7887)
    }
  },
  methods: {
    addLocalStorage() {
      localStorage.setItem('test', 1)
    },
    intervalTrigger() {
      return window.setInterval(() => {
        this.$refs.background.style.left = this.point.x-- + 'px'
      }, 1000)
    },
    initBackground() {
      this.$refs.background.style.top = this.point.y + 'px'
      this.$refs.background.style.left = this.point.x + 'px'
    },
    changeMapPos(e) {
      this.isMapEvent = true
      this.point = { x: e.clientX, y: e.clientY }
    },
  },
  watch: {},
}
</script>

<style scoped lang="scss">
.main-area {
  width: 100vw;
  height: 100vh;
  background: green;
  z-index: -1;
}

.background {
  width: 500px;
  height: 500px;
  background: lime;
  position: absolute;
  top: 0;
  left: 0;
  transition: all 0.5s ease-out 0s;
}
</style>

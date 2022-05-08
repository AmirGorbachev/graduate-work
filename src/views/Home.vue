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
    return {}
  },
  mounted() {
    document.onmousedown = (event) => {
      let shiftX =
        event.clientX - this.$refs.background.getBoundingClientRect().left
      let shiftY =
        event.clientY - this.$refs.background.getBoundingClientRect().top

      this.$refs.background.style.position = 'absolute'
      this.$refs.background.style.zIndex = 1000
      document.body.append(this.$refs.background)

      // переносит мяч на координаты (pageX, pageY),
      // дополнительно учитывая изначальный сдвиг относительно указателя мыши
      let moveAt = (pageX, pageY) => {
        if (this.$refs.background.style.left >= 0) {
          this.$refs.background.style.left = pageX - shiftX + 'px'
        }
        this.$refs.background.style.left = pageX - shiftX + 'px'
        this.$refs.background.style.top = pageY - shiftY + 'px'
      }

      let onMouseMove = (event) => {
        moveAt(event.pageX, event.pageY)
      }

      moveAt(event.pageX, event.pageY)

      // передвигаем мяч при событии mousemove
      document.addEventListener('mousemove', onMouseMove)

      // отпустить мяч, удалить ненужные обработчики
      document.onmouseup = () => {
        document.removeEventListener('mousemove', onMouseMove)
        this.$refs.background.onmouseup = null
      }
    }

    this.$refs.background.ondragstart = function () {
      return false
    }

    if (localStorage.getItem('test')) {
      console.log('store')
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
    changeMapPos() {},
  },
  watch: {},
}
</script>

<style scoped lang="scss">
.main-area {
  width: 100vw;
  height: 100vh;
  background: green;
  opacity: 0.7;
}

.background {
  width: 500px;
  height: 500px;
  background: lime;
  position: absolute;
  top: 50;
  left: 50;
  // transition: all 0.5s ease-out 0s;
}
</style>

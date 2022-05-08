<template lang="pug">
  div
    div.main-area(ref='main')
      div.background(ref='background' @mousedown='changeMapPos')
        Field
</template>

<script>
// @ is an alias to /src
import Field from '@/components/Field'

export default {
  name: 'home',
  components: {
    Field,
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
  background: url('../assets/sky.jpg');
}

.background {
  background: url('../assets/wood.jpg');
  position: absolute;
  top: 50;
  left: 50;
}
</style>

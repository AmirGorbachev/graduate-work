<template lang="pug">
  <div class="home">
    HelloWorld(msg="Welcome to Your Vue.js App")
    div.background(ref='background' @mousedown='changeMapPos')
    h5(@click.prevent='addLocalStorage') 88888888
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue';
import ProjectCard from '@/components/ProjectCard.vue';

export default {
  name: 'home',
  components: {
    HelloWorld,
    ProjectCard,
  },
  data() {
    return {
      top: 30,
      left: 25,
      isMapEvent: false,
      point: { x: 0, y: 0 },
    };
  },
  mounted() {
    this.initBackground();
    window.addEventListener('mouseup', this.mouseup);

    if (localStorage.getItem('test')) {
      console.log(7887);
    }
  },
  methods: {
    addLocalStorage() {
      localStorage.setItem('test', 1);
    },
    mouseup(e) {
      if (this.isMapEvent) {
        // console.log(e.target.onmousemove = null)
        const event = e
        console.log(event.target)
            console.log(this.$refs.background.clientX)

        this.$refs.background.removeEventListener(
          'mousemove',
          () => {
            console.log(this.$refs.background)
          }
        );

        this.isMapEvent = false;
      } else {
        console.log('not isMapEvent');
      }
    },
    initBackground() {
      this.$refs.background.style.top = this.point.y + 'px';
      this.$refs.background.style.left = this.point.x + 'px';
    },
    changeMapPos(e) {
      this.isMapEvent = true;
      this.point = { x: e.clientX, y: e.clientY };

      // this.$refs.background.addEventListener('mousemove', this.moveMap(event))
      this.$refs.background.addEventListener('mousemove', (event) => {
        this.$refs.background.style.top =
          this.top + (event.clientY - this.point.y) + 'px';
        this.$refs.background.style.left =
          this.top + (event.clientX - this.point.x) + 'px';
      });
    },
    moveMap(event) {
      this.$refs.background.style.top =
        this.top + (event.clientY - this.point.y) + 'px';
    },
  },
};
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

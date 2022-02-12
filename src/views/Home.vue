<template lang="pug">
  <div class="home">
    HelloWorld(msg="Welcome to Your Vue.js App")
    ProjectCard
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
  },
  mounted() {
    if (localStorage.getItem('test')) {
      console.log(7887);
    }
  },
  methods: {
    addLocalStorage() {
      localStorage.setItem('test', 1);
    },
  },
};
</script>

<style scoped lang="scss"></style>

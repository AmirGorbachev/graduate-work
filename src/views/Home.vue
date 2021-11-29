<template lang='pug'>
  <div class="home">
    HelloWorld(msg="Welcome to Your Vue.js App")
    ProjectCard
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
};
</script>

<style scoped lang="scss"></style>

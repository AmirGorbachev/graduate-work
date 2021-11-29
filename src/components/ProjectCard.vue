<template lang="pug">
  .project-card
    p ProjectCard
</template>

<script>
export default {
  name: 'ProjectCard',
  props: {
    msg: String,
  },
};
</script>

<style scoped lang="scss">
p {
  color: red;
}

.project-card {
  width: 280px;
  height: 560px;
  background: grey;
}
</style>

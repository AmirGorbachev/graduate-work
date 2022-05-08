<template lang="pug">
  .map
    //- Field
    Chess
</template>

<script>
import Field from '@/components/Field'
import Chess from '@/components/Chess'

export default {
  name: 'home',
  components: { Field, Chess },
  data() {
    return {
    }
  },
  mounted() {},
  methods: {},
  watch: {},
}
</script>

<style scoped lang="scss">
.map {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>

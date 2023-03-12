<template lang="pug">
  .main-area
    Kitchen
</template>

<script>
import Kitchen from '@/components/Kitchen'

export default {
  name: 'home',
  components: {
    Kitchen,
  },
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
.main-area {
  width: 100vw;
  height: 100vh;
  background: url('../assets/bg.svg') no-repeat;
  background-size: cover;
  background-position: center;
  cursor: url('../assets/cursor.svg'),auto;
}
</style>

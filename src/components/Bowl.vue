<template lang="pug">
.bowl
  Ingredient(v-for='item in items' :key='item.id' :title='item.title')
</template>

<script>
import Ingredient from '@/components/Ingredient'

export default {
  name: 'Bowl',
  components: {
    Ingredient,
  },
  props: {
    items: {
      type: Array,
      requiered: true,
    },
  },
  data() {
    return {
    }
  },
  methods: {
  },
}
</script>

<style scoped lang="scss">
.bowl {
  display: flex;
  gap: 20px;
  min-width: 50px;
  min-height: 50px;
  background-color: blue;
  padding: 15px;
}
</style>
